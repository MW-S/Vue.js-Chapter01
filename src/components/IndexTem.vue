<template>
  <div align="center">
    <p>{{msg}}</p>
    <div>
      <P>功能入口</P>
      <router-link class="btn btn-default btn-info" style="margin: 10px 20px; width: 120px;" to="/compare?choice=compareBool">{{param}}数字比较</router-link>
      <router-link class="btn btn-default btn-info" style="margin: 10px 20px; width: 120px;" to="/calculator?choice=calculatorBool">网页计算器</router-link>
    </div>
  </div>
</template>

<script>
export default {
  name: 'IndexTem',
  data () {
    return {
      msg: '欢迎来到Vue3.0实验一首页！'
    }
  }
}
</script>
