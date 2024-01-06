<template>
  <div class="content">
<div class="calculator">
    <div class="display">{{ display }}</div>
    <div>
      <div class="row">
        <div class="operation" v-for="operation of operations" :key="operation" @click="handleClickOnOperation(operation)">{{ operation }}</div>
      </div>
      <div class="row" v-for="subNumbers of numbers" :key="subNumbers">
        <div class="number" v-for="number of subNumbers" :key="number" @click="handleClickOnNumber(number)">
          {{ number }}
        </div>
      </div>
    </div>
  </div>
  </div>
</template>

<script setup>
  const numbers =[[7,8,9],[4,5,6],[1,2,3],[0]]
  const operations = ["+","AC","="]

  let args = []

  const display = ref("")

  const handleClickOnNumber = (clickedNumber)=>{
    display.value += clickedNumber 
  }

  const handleClickOnOperation = (operation)=>{
    if(operation=="+"){
      args.push(parseInt(display.value))
      display.value="";
    }
    else if(operation=="="){
      args.push(parseInt(display.value))
      let result = 0
      args.forEach((arg)=>{result+=arg})
      display.value = result;
    }
    else if(operation=="AC"){
      args=[];
      display.value=""
    }
  }

</script>

<style scoped>

  .content{
    display: flex;
    align-content: center;
  }
  .calculator{
    display: flex;
    flex-direction: column;
  }
  .row{ 
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;
  }
  .number{
    background-color: gray;
    margin: 5px;
    height: 30px;
    width: 30px;
    text-align: center; 
  }

  .display{
    height: 20px;
  }

  .operation{
    background-color: lightgray;
    margin: 5px;
    height: 30px;
    width: 30px;
    text-align: center;
    
  }
</style>
