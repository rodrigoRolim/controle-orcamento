<script>
  let debtOptions = [
    "Boletos",
    "Cartão de crédito",
    "Contas de casa",
    "Cmprestimos",
    "Consignados",
    "Carnês",
  ];
</script>

<div class="home">
  <h1>Escolha que tipos de dívidas você gostaria de cadastrar</h1>
  <div class="home__options">
    {#each debtOptions as debt}
      <div class="home__option card">
        { debt }
      </div>
    {/each}
  </div>
</div>

<style lang="scss">
.home {
  display: flex;
  flex-direction: column;
  align-items: center;
}
.home__options {
  display: flex;
  flex-wrap: wrap;
  gap: 16px;
  width: 500px;
  margin-top: 3rem;
}
.home__option {
  display: flex;
  justify-content: center;
  align-items: center;
  border: 1px solid;
  border-radius: 8px;
  width: 150px;
  height: 70px;
  cursor: pointer;
}
</style>
