<template>
  <div class="main" id="calculator" >
    <calculator></calculator>
  </div>
</template>

<script>
import calculator from '@/components/CalculatorTem.vue'
export default {
  map: 'calculator',
  components: {
    calculator
  }
}
</script>

<style lang="css">
  .main {
    height: 500px;
    box-shadow: 10px 10px 5px #bbb;
    background-color: #f8f8f8;
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .main div p {
    font-size: 30px;
  }
</style>
