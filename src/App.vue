<template>
  <div class="app">
    <calculator></calculator>
  </div>
</template>

<script>
import Calculator from './components/Calculator.vue'

export default {
  name: 'App',
  components: {
    Calculator,
  },
}
</script>

<style>
body {
  background: #ffeff2 !important;
}
</style>
