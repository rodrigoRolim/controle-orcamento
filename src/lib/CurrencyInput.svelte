<script>
  import { createEventDispatcher } from 'svelte';

  export let label
  export let debtValue = 0.00
  export let errorMessage = ''
  let currencyInput
  
  const dispatch = createEventDispatcher()
  function moneyMask(value) {
    value = value.replace(/\D/g, '')
    const options = { minimumFractionDigits: 2 }
    const result = new Intl.NumberFormat('pt-BR', options).format(parseFloat(value) / 100)

    return result
  }
  function toCurrency(e) {
    dispatch('update-debt-value', moneyMask(e.target.value))
  }
</script>

<label class="currency">
  <span>{label}</span>
  <div class="currency__input">
    <span>R$</span>
    <input 
      type="tel" 
      step="any" 
      min="0" 
      bind:value={debtValue} 
      bind:this={currencyInput} 
      on:input={toCurrency} 
    />
  </div>
  <small>{ errorMessage }</small>
</label>

<style lang="scss">
.currency {
  display: flex;
  flex-direction: column;
  & .currency__input {
    border: 1px solid;
    border-radius: 4px;
    & input {
      border: none;
      padding: 7px 5px;
    }
    & span {
      padding-left: 10px
    }
  }
}
</style>
