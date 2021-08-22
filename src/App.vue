<template>
  <h3>Form Validation Example</h3>
  <p>
    Name is required input & Lucky Number must be a nubmer
  </p>
  <div class="validation-check">
    <div v-if="!errors.length">
      <h3>Success!</h3>
      <p>This form is valid. No errors 😁👍</p>
    </div>
    <ul v-else>
      <li v-for="(error, key) in errors" :key="key">
        {{error}}
      </li>
    </ul>
  </div>
  <form @submit.prevent="handleSubmit">
    <input type="text" v-model="name" placeholder="Name">
    <input type="text" v-model="luckyNumber" placeholder="Lucky Number">
    <input type="submit" value="Submit">
  </form>
</template>

<script setup>
import { ref } from 'vue'

const name = ref('')
const luckyNumber = ref('')
const errors = ref([])
const validationState = ref('lime')

const handleSubmit = () => {
  errors.value = []

  if (!name.value.length > 0) {
    errors.value.push('Name is required')
  }
  
  if (luckyNumber.value.match(/\D/g)) {
    errors.value.push('Lucky number must be a number')
  }

  if (errors.value.length) {
    validationState.value = 'red'
  } else {
    validationState.value = 'lime'
  }
}
</script>

<style scoped>
.validation-check {
  padding: 2rem;
  background-color: v-bind('validationState')
}

* {
  font-family: Arial, Helvetica, sans-serif;
}

form {
  display: flex;
  flex-direction: column;
  margin-top: 50px;
}
input {
  margin-bottom: 5px;
  padding: 10px;
}

</style>
