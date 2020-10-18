<template>
  <div class="container" style="width: 300px;">
    <div class="row" align="center">
      <div class="showRes" style="height: 100px; border:aqua solid thin">
        <div class="showResInner" ><p>{{lastNum+sign+(currentNum==0?'':currentNum)}}</p></div>
        <div class="showResInner"><p>{{sign===''?lastNum:currentNum}}</p></div>
      </div>
    </div>
    <div class="row"  >
        <buttun style="font-size: 25px;" class="btn btn-default col-md-3" @click ="clear()">CE</buttun>
        <buttun style="font-size: 25px;" class="btn btn-default col-md-3" @click ="this.lastNum !== '除数不能为0！' ? minus() :''">←</buttun>
        <buttun style="font-size: 25px;" class="btn btn-default col-md-3" @click ="this.lastNum !== '除数不能为0！' ? change('+') : ''">+</buttun>
        <buttun style="font-size: 25px;" class="btn btn-default col-md-3" @click = "this.lastNum !== '除数不能为0！' ? change('-') : ''">﹣</buttun>
    </div>
    <div class="row" v-for="item in 4" >
        <buttun style="font-size: 25px;" class="btn btn-default col-md-3" @click ="10-3*item > 0 ? isLastNum (10-3*item) : isLastNum (0)">
          {{10-3*item > 0 ? 10-3*item : 0}}
        </buttun>
        <buttun style="font-size: 25px;" class="btn btn-default col-md-3" @click ="11-3*item > 0 ? isLastNum(11-3*item) : isLastNum('.')">
          {{11-3*item > 0 ? 11-3*item : '.'}}
        </buttun>
        <buttun style="font-size: 25px;" class="btn btn-default col-md-3" @click ="12-3*item > 0 ? isLastNum(12-3*item): calculator()">
          {{12-3*item > 0 ? 12-3*item : '='}}
        </buttun>
        <buttun style="font-size: 25px;" class="btn btn-default col-md-3" @click = " this.lastNum !== '除数不能为0！' ? sign= ['/','*','-','+'][item-1] : ''">
          {{['/','*','-','+'][item-1]}}
        </buttun>
      </div>
    </div>
</template>

<script>
export default {
  name: 'CalculatorTem',
  data () {
    return {
      msg: 'calculatorTemplate',
      lastRes: 0,
      lastNum: 0,
      currentNum: 0,
      calCount: 0,
      sign: ''
    }
  },
  methods: {
    calculator () {
      this.calCount++
      var res = 0
      console.log(this.sign, this.currentNum)
      if (this.sign == '/' && this.currentNum == 0) {
        res = '除数不能为0！'
        this.clear()
        this.lastNum = res
      } else if (this.sign !== '') {
        res = eval('(' + this.lastNum + ')' + this.sign + '(' + String(this.currentNum) + ')')
        this.clear()
        this.lastNum = res
      } else {
        console.log(String(this.lastNum).indexOf('.'))
        if (String(this.lastNum).indexOf('.') === 0) {
          this.lastNum = 0 + this.lastNum
        } else if (String(this.lastNum).indexOf('.') === (String(this.lastNum).length - 1)) {
          this.lastNum += 0
        }
        res = eval('(' + this.lastNum + ')')
      }
      console.log(res)
      return res
    },
    isLastNum (num) {
      console.log(num)
      if (this.sign === '') {
        if ((this.lastNum === 0 || this.lastNum === '除数不能为0！') && num !== '.') {
          this.lastNum = num
        } else {
          if (this.calCount > 0) {
            this.lastNum = num
            this.calCount = 0
          } else {
            if (num === '.') {
              if (String(this.lastNum).indexOf(num) === -1) {
                this.lastNum += '' + num
              }
            } else {
              this.lastNum += '' + num
            }
          }
        }
      } else {
        if (this.currentNum === 0) {
          this.currentNum = num
        } else {
          if (num === '.') {
            if (String(this.currentNum).indexOf(num) === -1) {
              this.currentNum += '' + num
            }
          } else {
            this.currentNum += '' + num
          }
        }
      }
    },
    clear () {
      this.lastNum = 0
      this.currentNum = ''
      this.sign = ''
      this.calCount = 0
    },
    minus () {
      if (this.currentNum !== '' && this.currentNum > 0) {
        this.currentNum = String(this.currentNum)
        this.currentNum = this.currentNum.substr(0, this.currentNum.length - 1)
        console.log('currentNum：' + this.currentNum)
      } else if (this.sign !== '') {
        this.sign = ''
      } else {
        this.lastNum = String(this.lastNum)
        this.lastNum = this.lastNum.substr(0, this.lastNum.length - 1)
        if (this.lastNum === '') {
          this.lastNum = 0
        }
        console.log('lastNum：' + this.lastNum)
      }
    },
    change (sign) {
      var head = ''
      if (this.currentNum !== '' && this.currentNum > 0) {
        this.currentNum = String(this.currentNum)
        head = this.currentNum.substr(0, 1)
        if (head !== '-' && sign === '-') {
          this.currentNum = '-' + this.currentNum
        } else if (head === '-' && sign === '+') {
          this.currentNum = this.currentNum.replace(head, '')
        }
        console.log('currentNum：' + this.currentNum)
      } else if (this.sign !== '') {
        head = ''
      } else {
        if (this.lastNum === 0) {
          return
        }
        this.lastNum = String(this.lastNum)
        head = this.lastNum.substr(0, 1)
        if (head !== '-' && sign === '-') {
          this.lastNum = '-' + this.lastNum
        } else if (head === '-' && sign === '+') {
          this.lastNum = this.lastNum.replace(head, '')
        }
        console.log('lastNum：' + this.lastNum)
      }
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

<style lang="css">
  .showResInner{
    display: flex;
    flex-direction: row-reverse;
    padding: 0px 15px;
  }
</style>
