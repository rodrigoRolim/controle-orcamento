<script>
  import "../app.css"
  import { total } from "../store"

  let billValueTotal = 0
  total.subscribe((data) => {
    const options = { minimumFractionDigits: 2 }
    billValueTotal = new Intl.NumberFormat('pt-BR', options).format(data)
  })

</script>
<div class="main">
  <div class="main__total">Total: { billValueTotal }</div>
  <slot/>
</div>

<style lang="scss">
.main {
  max-width: 1220px;
  margin: 0 auto;
  padding: 5rem 1rem;
  & .main__total {
    margin-bottom: 2rem;
    font-weight: 500;
  }
}
</style>