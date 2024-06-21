<script setup>
const emit = defineEmits(['resetCount'])
function resetEmit() {
  emit('resetCount', 100)
}
</script>

<template>
  <button @click="$emit('resetCount', 100)">Reset</button>
  <button @click="resetEmit">Reset</button>
</template>
