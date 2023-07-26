<script>
  import CurrencyInput from "../../lib/CurrencyInput.svelte";
  import { total } from "./../../store";

  let description = '';
  let isDescriptionValid = true;
  let value;
  let isValueValid = true;
  let bills = []
  
  function calcTotal() {
    total.update(() => {
      return bills
        .map(bill => bill.value.replace('.', ''))
        .map(bill => bill.replace(',', '.'))
        .reduce((acc, currentValue) => acc + Number(currentValue), 0)
    })
  }
 
  
  function addBill() {
    if (!validateFields()) {
      alert('preencha os campos obrigatórios');
      return;
    }
    const bill = { description, value, id: Date.now() + value }
    bills = [ bill, ...bills]
    calcTotal()
    description = ''
    value = 0
  }
  function updateDebtValue(newDebtValue) {
    console.log(newDebtValue)
    value = newDebtValue.detail
  }
  function validateFields() {
    isDescriptionValid = isDescriptionValid !== ''
    isValueValid = value !== ''

    return isDescriptionValid && isValueValid
  }
</script>

<div class="bill">
  <div class="bill__add">
    <label class="bill__input bill__description">
      <span>descrição:</span>
      <input type="text" bind:value={description} />
      <small>{ !isDescriptionValid ? 'campo obrigatório' : '' }</small>
    </label>
    <CurrencyInput 
      label="valor" 
      bind:debtValue={value} 
      on:update-debt-value={updateDebtValue}
      error-message={ !isValueValid ? 'campo obrigatório' : '' }
    />
    <button 
      class="bill__button"
      on:click={addBill}
    >salvar</button>
  </div>
  <table class="bill__table">
    <thead>
      <tr>
        <th>Descrição</th>
        <th>Valor R$</th>
      </tr>
    </thead>
    <tbody>
      {#each bills as bill (bill.id)} 
        <tr>
          <td>{ bill.description }</td>
          <td>{ bill.value }</td>
        </tr>
      {/each}
    </tbody>
  </table>
</div>
<style lang="scss">
.bill__add {
  display: flex;
  justify-content: space-between;
  align-items: flex-end;
  & .bill__button {
    width: 13%;
    height: 39px;
  } 
}
.bill__input {
  display: flex;
  flex-direction: column;
  &.bill__description {
    position: relative;
    width: 60%;
    & small {
      position: absolute;
      bottom: -20px;
    }
  }
  &.bill__value {
    width: 25%
  }
}
.bill__table {
  margin-top: 2rem;
}
</style>