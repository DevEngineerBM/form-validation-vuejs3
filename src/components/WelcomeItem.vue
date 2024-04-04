<template>
  <form @submit.prevent="submitForm" class="custom-fom">
    <!-- NAME FORM -->
    <div class="form-group">
      <label for="name">Name:</label>
      <input type="text" v-model="formData.name" id="name" />
      <span v-if="!isNameValid" class="error">name is requered</span>
    </div>

    <!-- EMAIL FORM -->
    <div class="form-group">
      <label for="email">email:</label>
      <input type="text" v-model="formData.email" id="email" />
      <span v-if="!isEmailValid" class="error">enter valid email adress</span>
    </div>

    <!-- PASSWORD FORM -->
    <div class="form-group">
      <label for="password">password:</label>
      <input type="text" v-model="formData.password" id="password" />
      <span v-if="!isPassWordValid" class="error">password must be at least a 8 caracters</span>
    </div>

    <button type="submit" :disabled="!isFormValid">submit</button>
  </form>
</template>

<script setup>
import { ref, computed } from 'vue'

/* DATA REFERENCE */
const formData = ref({
  name: '',
  email: '',
  password: ''
})

/* VALIDATION CRITERIAT */
const isNameValid = computed(() => formData.value.name.trim() != '')
const isEmailValid = computed(() => /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(formData.value.email))
const isPassWordValid = computed(() => formData.value.password.length >= 8)
const isFormValid = computed(() => isNameValid.value && isEmailValid && isPassWordValid.value)

/* SUBMIT */
const submitForm = () => {
  if (isFormValid.value) {
    alert('form Submitted', formData.value)
    formData.value = { name: '', email: '', password: '' }
  } else {
    alert('form is invalid please check fields')
  }
}
</script>

<style scoped>
form {
  display: flex;
  flex-direction: column;
  align-items: center;
  max-width: 600px;
  margin: 0 auto;
  padding: 20px;
  background-color: #f8f9fa;
  border-radius: 5px;
}

.form-group {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  width: 80%;
  margin-bottom: 25px;
}

label {
  font-weight: bold;
  margin-bottom: 10px;
  color: #2c3e50;
}

input {
  width: 100%;
  padding: 15px;
  font-size: 18px;
  border: 1px solid #bdc3c7;
  border-radius: 5px;
}

.error {
  color: #e74c3c;
  font-size: 16px;
  margin-top: 10px;
}

button[type='submit'] {
  width: 100%;
  padding: 15px 20px;
  font-size: 18px;
  background-color: #3498db;
  color: #fff;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

button[type='submit']:disabled {
  background-color: #bdc3c7;
  cursor: not-allowed;
}
</style>
