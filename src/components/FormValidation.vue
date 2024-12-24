<script setup>
import { ref, computed } from "vue";

const formData = ref({
    name: "",
    email: "",
    password: ""
})

const isNameValid = computed(() => formData.value.name.trim() !== "")
const isEmailValid = computed(() => /^[^\s@]+@[^\s@]+\.[^\s@]{2,}$/.test(formData.value.email))
const isPasswordValid = computed(() => formData.value.password.length >= 8)
const isFormValid = computed(() => isNameValid.value && isEmailValid.value && isPasswordValid)

const submitForm = () => {
    if (isFormValid.value) {
        console.log('form submitted',formData.value);
    } else {
        console.log('form is invalid. Please check the inputs');
    }
}
</script>


<template>
    <div>
        <form @submit.prevent="submitForm" class="custom-form">
            <h1>Register Form</h1>
            <!-- NAME FIELD -->
            <div class="form-group">
                <label for="name">Name:</label>
                <input type="text" id="name" v-model="formData.name" class="">
                <span v-if="!isNameValid" class="error">Name is required</span>
            </div>
            <!-- EMAIL FIELD -->
            <div class="form-group">
                <label for="email">Email:</label>
                <input type="email" id="email" v-model="formData.email" class="">
                <span v-if="!isEmailValid" class="error">Email is required</span>
            </div>
            <!-- PASSWORD FIELD -->
            <div class="form-group">
                <label for="password">Password:</label>
                <input type="password" id="password" v-model="formData.password" class="">
                <span v-if="!isPasswordValid" class="error">Password must be at least 8 characters</span>
            </div>

            <button type="submit" :disabled="!isFormValid" class="submit-button">SUBMIT</button>
        </form>
    </div>
</template>


<style scoped>
.custom-form {
  width: 550px;
  margin: 50px auto;
  padding: 20px;
  background-color: #f9f9f9;
  border-radius: 8px;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.3);
  font-family: Arial, sans-serif;
}

.form-group {
  margin-bottom: 20px;
}

label {
  display: block;
  font-weight: bold;
  margin-bottom: 8px;
  color: #333;
}

input {
  width: 100%;
  padding: 10px;
  font-size: 14px;
  border: 1px solid #ccc;
  border-radius: 4px;
  transition: border-color 0.3s ease;
}

input:focus {
  border-color: #007bff;
  outline: none;
}

.error {
  display: block;
  margin-top: 5px;
  font-size: 12px;
  color: #d9534f;
}

.submit-button {
  width: 100%;
  padding: 10px;
  font-size: 16px;
  color: white;
  background-color: #17be25;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.submit-button:hover {
  background-color: #06851b;
}

/* .submit-button:disabled {
  background-color: #ccc;
  cursor: not-allowed;
} */
</style>
