<template>
  <div align="center">
    <div class="compareNumber">
      <div>
        <label>数字一：</label>
        <input class="form-control" style="width: 150px;" type="number" v-model="numberOne" name="number" id="numberOne" placeholder= "请输入第一个数字" />
      </div>
      <div>
        <label>数字二：</label>
        <input class="form-control" style="width: 150px;" type="number" v-model="numberTwo" name="number" id="numberTwo" placeholder="请输入第二个数字" />
      </div>
    </div>
    <div class="compareNumber">
      <label>数字比较结果：{{maxNumber}}</label>
    </div>
    <a class="btn btn-default btn-info" @click="numberTwo=numberOne=''">清空数字</a>
  </div>
</template>

<script>
export default {
  name: 'CompareTem',
  data () {
    return {
      msg: 'compareTemplate',
      numberOne: '',
      numberTwo: ''
    }
  },
  computed: {
    maxNumber () {
      var one = parseInt(this.numberOne)
      var two = parseInt(this.numberTwo)
      var res = one >= two ? one : two
      console.log(isNaN(res))
      res = (isNaN(res) ? '' : res)
      return res
    }
  },
  beforeCreate () {
    console.log(this.$route)
    var co = this.$route.query.choice
    if (co === 'compareBool') {
      this.$root.$data.choice = 'compare'
    } else if (co === 'calculatorBool') {
      this.$root.$data.choice = 'calculator'
    }
  }
}
</script>

<style>
</style>
