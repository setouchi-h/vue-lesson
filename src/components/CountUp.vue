<script setup>
import { ref } from 'vue'

const count = ref(0)

function countUp() {
  count.value++
}
</script>

<template>
  <h2 v-bind="$attrs">CountUp</h2>
  <p>{{ count }}</p>
  <BaseIcon />
  <button @click="countUp">+</button>
</template>
