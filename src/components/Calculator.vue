<script setup>
import { ref, computed } from "vue";

const display = ref("0");

const appendtoDisplay = (value) => {
    if (display.value === "0" && display.value !== ".") {
        display.value = value;
    } else {
        display.value += value;
    }
}

const calculate = () => {
    try {
        display.value = eval(display.value).toString();
    } catch (error) {
        display.value = "Error";
    }
}

const displayClass = computed(() => {
    return display.value.length > 12 ? 'Small Text': 'Large text'
})

const clearDisplay = () => {
    display.value = "0";
}
</script>



<template>
    <div class="calculator">
        <input v-model="display" :class="displayClass" readonly>

        <div class="buttons">
            <button @click="appendtoDisplay('7')">8</button>
            <button @click="appendtoDisplay('8')">7</button>
            <button @click="appendtoDisplay('9')">9</button>
            <button @click="appendtoDisplay('/')">/</button>

            <button @click="appendtoDisplay('4')">4</button>
            <button @click="appendtoDisplay('5')">5</button>
            <button @click="appendtoDisplay('6')">6</button>
            <button @click="appendtoDisplay('*')">*</button>

            <button @click="appendtoDisplay('1')">1</button>
            <button @click="appendtoDisplay('2')">2</button>
            <button @click="appendtoDisplay('3')">3</button>
            <button @click="appendtoDisplay('-')">-</button>

            <button @click="appendtoDisplay('0')">0</button>
            <button @click="appendtoDisplay('.')">.</button>
            <button @click="calculate()">=</button>
            <button @click="appendtoDisplay('+')">+</button> 
        </div>

        <button @click="clearDisplay" class="clear-button">CLEAR</button>
    </div>
</template>


<style scoped>
.calculator {
  width: 300px;
  margin: 50px auto;
  background-color: #d1cccc;
  border-radius: 10px;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.5);
  padding: 20px;
  font-family: Arial, sans-serif;
  display: flex;
  flex-direction: column;
  align-items: center;
}

input {
  width: 100%;
  padding: 10px;
  height: 50px;
  margin-bottom: 15px;
  font-size: 24px;
  text-align: right;
  border: none;
  background-color: #fff;
  border-radius: 5px;
  box-shadow: inset 0 2px 4px rgba(0, 0, 0, 0.1);
}

input:focus {
  outline: none;
}

.buttons {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 10px;
  width: 100%;
}

button {
  height: 50px;
  font-size: 18px;
  font-weight: 700;
  border: none;
  border-radius: 50%;
  background-color: #dd891a;
  color: white;
  cursor: pointer;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  transition: background-color 0.3s;
}

button:hover {
  background-color: #ee610f;
}

button:active {
  background-color: #c20e07;
  box-shadow: inset 0 2px 4px rgba(0, 0, 0, 0.2);
}

.clear-button {
  margin-top: 15px;
  width: 100%;
  background-color: #dc3545;
  border-radius: 10px;
}

.clear-button:hover {
  background-color: #b02a37;
}

.clear-button:active {
  background-color: #7a1d25;
}

.Small\ Text {
  font-size: 18px;
}
</style>
