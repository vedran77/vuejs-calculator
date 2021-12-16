<template>
  <Calculator/>
</template>

<script lang="ts">
import { Options, Vue } from 'vue-class-component';
import Calculator from './components/Calculator.vue';

@Options({
  components: {
    Calculator
  },
})
export default class App extends Vue {}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Nunito:wght@200&display=swap');

body {
  background-image: linear-gradient(to right, #b5b5b5, #d9d9d9);
}

</style>
