<template>
  <div id="app">
    <div class="example">
      <button @click="isPay=true">点击弹出支付键盘</button>
    </div>
    <vue-pixel-keyboard ref="pay" :is-pay='isPay' @pas-end='pasEnd' @close='isPay=false' :keyList=keyList :num=num>
    </vue-pixel-keyboard>
  
  </div>
</template>

<script>
// import {vuePixelKeyboard} from 'vue-pixel-keyboard' //引用module包形式
import {vuePixelKeyboard} from './vuePixelKeyboard' //应用本地组件
export default {
  name: 'app',
  data() {
    return {
      isPay: false,
      // keyList: [
      //   [0,4,5],
      //   [2,9,1],
      //   [8,6,7]
      // ],
      // num:'3',
      keyList: [
        [{key:0,value:1},{key:3,value:2},{key:5,value:3}],
        [{key:2,value:4},{key:9,value:5},{key:1,value:6}],
        [{key:8,value:7},{key:6,value:8},{key:7,value:9}]
      ],
      num:{key:4,value:0}
    }
  },
  components:{
    vuePixelKeyboard
  },
  methods: {
    pasEnd(val) {
      console.log(val);  //得到密码 可能会进行一些加密动作
      setTimeout(() => { // 模拟请求接口验证密码中 .. 
        if (val === '111111') {
          this.$refs.pay.$payStatus(true) // 传递给子组件
        } else {
          this.$refs.pay.$payStatus(false)
        }
      }, 1000)
    }
  }
}
</script>

<style lang="scss">
.example {
  text-align: center;
  margin-bottom: 20px;
  button {
    border: 1px solid #ccc;
    height: 30px;
    background: #fff;
  }
}
</style>