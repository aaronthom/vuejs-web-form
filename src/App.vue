<template>
  <SignupForm />
</template>

<script>
import SignupForm from './components/SignupForm.vue'

export default {
  components: {
    SignupForm
  }
}
</script>

<style>
#app {
  font-family: Arial, Helvetica, sans-serif;

  text-align: center;

  color: #2c3e50;

  margin-top: 60px;
}

body {
  margin: 0;
  padding: 0;
  background: #eee;
}
</style>
