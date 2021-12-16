<template>
  <div class="number">
    <p>{{ number }}</p>
  </div>
</template>

<script lang="ts">
import { Options, Vue } from 'vue-class-component';

@Options({
  props: {
    number: Number
  }
})

export default class Number extends Vue {
  number!: number
}
</script>

<style scoped>
.number {
  display: flex;
  justify-content: center;
  align-items: center;
  background: #ebe7e4;
  z-index: -1;
  text-align: center;
  font-family: 'Nunito', sans-serif;
}

.number:hover {
    cursor: pointer;
}
</style>
