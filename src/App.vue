<script setup>
import { ref, computed, watch } from 'vue';
import InputKey from "@/InputKey.vue";
import OperationKey from "@/OperationKey.vue";

const accumulated = ref('0');
const operation = ref('');
const input = ref('0');
const accumulatedNum = computed(() => { return Number(accumulated.value) })
const inputNum = computed(() => { return Number(input.value) })

function handleInput(pressedKey) {
  if(!inputNum.value) input.value = pressedKey;
  else input.value += pressedKey;
}

function handleOperation(pressedKey) {
  switch (pressedKey) {
    case "C":
      accumulated.value = '0';
      operation.value = '';
      input.value = '0';
      break;
    case "=":
      doTheMath();
      break;
    default:
      doTheMath();
      operation.value = pressedKey;
      input.value = '0';
      break;
  }
}

function doTheMath() {
  let result = 0;
  switch (operation.value) {
    case "+":
      result = accumulatedNum.value + inputNum.value;
      break;
    case "-":
      result = accumulatedNum.value - inputNum.value;
      break;
    case "×":
      result = accumulatedNum.value * inputNum.value;
      break;
    case "÷":
      result = accumulatedNum.value / inputNum.value;
      break;
    default:
      result = inputNum.value;
  }
  accumulated.value = result.toString();
}

</script>
<template>
  <div class="app h-screen flex justify-center items-center">
    <div class="rounded border border-white bg-slate-600 p-4 w-fit h-fit">
      <div class="rounded bg-green-600 p-1 text-end mb-5">
        <div class="text-xs">{{ accumulated }} {{ operation }}</div>
        <div class="text-3xl font-bold">{{ input }}</div>
      </div>
      <div class="grid grid-cols-4 grid-rows-5 gap-x-1 gap-y-2 buttons-grid">
        <OperationKey value="C" @press-key="handleOperation"></OperationKey>
        <OperationKey value="÷" @press-key="handleOperation"></OperationKey>
        <InputKey value="7" @press-key="handleInput"></InputKey>
        <InputKey value="8" @press-key="handleInput"></InputKey>
        <InputKey value="9" @press-key="handleInput"></InputKey>
        <OperationKey value="×" @press-key="handleOperation"></OperationKey>
        <InputKey value="4" @press-key="handleInput"></InputKey>
        <InputKey value="5" @press-key="handleInput"></InputKey>
        <InputKey value="6" @press-key="handleInput"></InputKey>
        <OperationKey value="-" @press-key="handleOperation"></OperationKey>
        <InputKey value="1" @press-key="handleInput"></InputKey>
        <InputKey value="2" @press-key="handleInput"></InputKey>
        <InputKey value="3" @press-key="handleInput"></InputKey>
        <OperationKey value="+" @press-key="handleOperation"></OperationKey>
        <InputKey value="0" @press-key="handleInput"></InputKey>
        <InputKey value="." @press-key="handleInput"></InputKey>
        <OperationKey value="=" @press-key="handleOperation"></OperationKey>
      </div>
    </div>
  </div>
</template>
