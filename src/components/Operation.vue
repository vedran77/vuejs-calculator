<template>
  <div class="operation">
    <p>{{ operation }}</p>
  </div>
</template>

<script lang="ts">
import { Options, Vue } from 'vue-class-component';

@Options({
  props: {
    operation: String
  }
})

export default class Operation extends Vue {
  operation!: string
}
</script>

<style scoped>
.operation {
    display: flex;
    justify-content: center;
    background: #ebe7e4;
    z-index: -1;
    text-align: center;
}

.operation p {
    display: flex;
    justify-content: center;
    align-items: center;
    background: #565859;
    border-radius: 50%;
    text-align: center;
    width: 40px;
    height: 40px;
    font-size: 18px;
    font-family: 'Nunito', sans-serif;
    color: #fff;
}

.operation:hover {
    cursor: pointer;
}
</style>
