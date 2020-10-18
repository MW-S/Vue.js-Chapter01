<template>
  <div class="main"  id="compare">
    <compare></compare>
  </div>
</template>

<script>
import compare from '@/components/CompareTem.vue'
export default {
  map: 'compare',
  components: {
    compare
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
