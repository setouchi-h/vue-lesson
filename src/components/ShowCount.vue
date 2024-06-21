<script setup>
const props = defineProps(['foo'])
console.log(props.foo) // reactiveなデータ
</script>
<template>
  <p>count: {{ foo }}</p>
</template>
