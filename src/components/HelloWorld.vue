<script setup>
import { ref } from 'vue'
const x1 = ref([])
const num = ref('')
//算式的第一个数字
const firstNum = ref()
//算式的第二个数字
const secondNum = ref()

//获取鼠标按下的值
function getvalue(e) {
  num.value += e.target.value
  x1.value.splice(0, 1, num.value)
}

//清除input框中的值
function clearAll() {
  x1.value = [];
  num.value = ''
}

//删除一个刚刚输入的值（回退）
function backLast() {
  num.value = num.value.substring(0, num.value.length - 1)
  x1.value.splice(0, 1, num.value)
  console.log(x1.value);


}

// 输出到input框
function calculator() {
  return x1.value
}

//计算（等于）
function theResult() {
  // 加法
  const add = num.value.indexOf('+')

  // 减法
  const subtract = num.value.indexOf('-')

  // 乘法
  const multiply = num.value.indexOf('*')
  //除法
  const division = num.value.indexOf('/')
  if (add != -1) {
    firstNum.value = (num.value.slice(0, add)) * 1
    secondNum.value = (num.value.slice(add + 1)) * 1
    num.value = (firstNum.value + secondNum.value).toString()
    x1.value[0] = num.value
  }
  else if (subtract != -1) {
    firstNum.value = (num.value.slice(0, subtract)) * 1
    secondNum.value = (num.value.slice(subtract + 1)) * 1
    num.value = (firstNum.value - secondNum.value).toString()
    x1.value[0] = num.value
  }
  else if (multiply != -1) {
    firstNum.value = (num.value.slice(0, multiply)) * 1
    secondNum.value = (num.value.slice(multiply + 1)) * 1
    num.value = (firstNum.value * secondNum.value).toString()
    x1.value[0] = num.value
  }
  else if (division != -1) {
    firstNum.value = (num.value.slice(0, division)) * 1
    secondNum.value = (num.value.slice(division + 1)) * 1
    num.value = (firstNum.value / secondNum.value).toString()
    x1.value[0] = num.value
  }
}

</script>

<template>
  <div class="box">
    <input type="text" :value="calculator()">
    <div class="calc">
      <button class="op_key" @click="clearAll">AC</button>
      <button class="op_key" @click="backLast">bc</button>
      <button class="op_key" @click="getvalue($event)" value="%">%</button>
      <button class="op_key" @click="getvalue($event)" value="/">/</button>
      <button class="num_key" @click="getvalue($event)" value="7">7</button>
      <button class="num_key" @click="getvalue($event)" value="8">8</button>
      <button class="num_key" @click="getvalue($event)" value="9">9</button>
      <button class="op_key" @click="getvalue($event)" value="*">*</button>
      <button class="num_key" @click="getvalue($event)" value="4">4</button>
      <button class="num_key" @click="getvalue($event)" value="5">5</button>
      <button class="num_key" @click="getvalue($event)" value="6">6</button>
      <button class="op_key" @click="getvalue($event)" value="-">-</button>
      <button class="num_key" @click="getvalue($event)" value="1">1</button>
      <button class="num_key" @click="getvalue($event)" value="2">2</button>
      <button class="num_key" @click="getvalue($event)" value="3">3</button>
      <button class="op_key" @click="getvalue($event)" value="+">+</button>
      <button class="op_key">bt</button>
      <button class="num_key" @click="getvalue($event)" value="0">0</button>
      <button @click="getvalue($event)" value=".">.</button>
      <button class="op_key" @click="theResult">=</button>
    </div>
  </div>
</template>

<style scoped lang="less">
.box {
  margin: auto;
  width: 200px;
  height: 300px;
  background-color: skyblue;

  input {
    margin: auto;
    width: 200px;
  }

  .calc {
    display: flex;
    flex-wrap: wrap;

    button {
      width: 50px;
      height: 50px;
    }
  }

}
</style>
