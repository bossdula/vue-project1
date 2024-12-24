<script setup>
import { ref } from "vue";

const passwordLength = ref(12);
const includeUppercase = ref(true);
const includeNumbers = ref(true);
const includeSymbols = ref(true);
const generatedPassword = ref("")

const generatePassword = () => {
    const lowercaseChars = "abcdefghijklmnopqrstuvwxyz"
    const uppercaseChars = includeUppercase.value ? "ABCDEFGHIJKLMNOPQRSTUVWXYZ" : "";
    const numberChars = includeNumbers.value ? "0123456789" : "";
    const symbolChars = includeSymbols.value ? "!@#$%^&*().,[]{}\/?~" : "";

    const allChars = lowercaseChars + uppercaseChars + numberChars + symbolChars;

    let password = "";

    for (let i = 0; i < passwordLength.value; i++) {
        const randomIndex = Math.floor(Math.random() * allChars.length);
        password += allChars[randomIndex];  
    }

    generatedPassword.value = password;
}
</script>

<template>
    <div class="password-generator-container">
        <h2 class="password-generator-title">Password Generator</h2>

        <label for="length">Password Length</label>
        <input type="number" id="length" v-model="passwordLength" min="4" max="32">
        <br>

        <label for="includeUppercase">Include Uppercase:</label>
        <input type="checkbox" id="includeUppercase" v-model="includeUppercase">
        <br>

        <label for="includeSymbols">Include Symbols:</label>
        <input type="checkbox" id="includeSymbols" v-model="includeSymbols">
        <br>

        <label for="includeNumbers">Include Numbers:</label>
        <input type="checkbox" id="includeNumbers" v-model="includeNumbers">
        <br>

        <button @click="generatePassword" class="geenrate-button">Generate Password</button>

        <div v-if="generatePassword">
            <strong>Your Password is: </strong>{{ generatedPassword }}
        </div>
    </div>
</template>

<style scoped>
.password-generator-container {
  width: 450px;
  margin: 50px auto;
  padding: 20px;
  background: #8f8eb8;
  border: 1px solid #f36eec;
  border-radius: 10px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.5);
  font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
}

.password-generator-title {
  text-align: center;
  font-size: 1.8em;
  color: #fff;
  margin-bottom: 15px;
}

label {
  font-weight: bold;
  color: #fff;
  display: block;
  margin-bottom: 5px;
}

input[type="number"],
input[type="checkbox"] {
  margin-bottom: 12px;
}

input[type="number"] {
  width: 50%;
  padding: 8px;
  border: 1px solid #ccc;
  border-radius: 5px;
  font-size: 1em;
}

input[type="checkbox"] {
  margin-left: 5px;
  transform: scale(1.2);
}

.geenrate-button {
  display: block;
  width: 100%;
  padding: 10px 15px;
  background-color: #4caf50;
  color: #fff;
  font-size: 1em;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.geenrate-button:hover {
  background: #45a049;
}

div {
  margin-top: 15px;
  text-align: center;
  font-size: 1.1em;
}

strong {
  color: #080808;
}
</style>
