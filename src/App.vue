<template>
<div class="rows">
  <div class="inputs">
    <div>
      <input type="number" class="inputBox" v-model="num1" />
    </div>
    <div>
      <select v-model="operator" class="operatorBox">
        <option selected value="+">+</option>
        <option value="-">-</option>
        <option value="*">*</option>
        <option value="/">/</option>
        <option value="^">^</option>
      </select>
    </div>
    <div>
      <input type="number" class="inputBox" v-model="num2"/>
    </div>
    <div>
      <h1>=</h1>
    </div>
    <div>
      <h1 class="sum">{{result}}</h1>
    </div>
  </div>
</div>
</template>

<script>
import { reactive, computed, toRefs } from 'vue';

function useSum() {
  let state = reactive({
    num1: 0,
    num2: 0,
    operator: null,
    result: null,
  })

  state.result = computed(() =>  {
    if(state.operator){
      if(state.operator == '-'){
        return parseInt(state.num1) - parseInt(state.num2)
      }
      if(state.operator == '+'){
        return parseInt(state.num1) + parseInt(state.num2)
      }
      if(state.operator == '*'){
        return parseInt(state.num1) * parseInt(state.num2)
      }
      if(state.operator == '/'){
        return parseInt(state.num1) / parseInt(state.num2)
      }
      if(state.operator == '^'){
        return Math.pow(state.num1, state.num2);
      }
    }
  })

  return toRefs(state)
}
export default {
  name: "Calculator",

  setup(){
    let { num1 , num2, result, operator } = useSum();

    return {
      num1,
      num2,
      result,
      operator,
    }
  }

}


</script>

<style>
#app {
  display: flex;
  flex-grow: 1;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  justify-content: center;
  align-items: center;
  color: #2c3e50;
  margin-top: 60px;
}

.inputs{
  display: flex;
  flex-direction: row;
  align-items: center;
}

.inputBox{
  height: 60px;
  width: 60px;
  margin-right: 30px;
  margin-left: 30px;
  text-align: center;
  font-size: 24pt;
  font-weight: bold;
}
.operatorBox{
  height: 60px;
  width: 60px;
  text-align: center;
  font-size: 24pt;
  font-weight: bold;
}
.sum{
  width: 60px;
  height: 60px;
  /* outline: 1px solid black; */
  display: flex;
  align-items: center;
  justify-content: center;
}
.rows{
  display: flex;
  flex-direction: column;
  width: 100vw;
  justify-content: center;
  align-items: center;
}



/* Chrome, Safari, Edge, Opera */
input::-webkit-outer-spin-button,
input::-webkit-inner-spin-button {
  -webkit-appearance: none;
  margin: 0;
}

/* Firefox */
input[type=number] {
  -moz-appearance: textfield;
}
</style>
