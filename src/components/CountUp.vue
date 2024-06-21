<script setup>
import {
  ref,
  onBeforeMount,
  onMounted,
  onBeforeUpdate,
  onUpdated,
  onBeforeUnmount,
  onUnmounted,
  nextTick
} from 'vue'

const count = ref(0)

onBeforeMount(() => {
  console.log('beforeMount')
})
onMounted(() => {
  console.log('mounted')
})
onBeforeUpdate(() => {
  console.log('beforeUpdate')
})
onUpdated(() => {
  console.log('updated')
})
onBeforeUnmount(() => {
  console.log('beforeUnmount')
})
onUnmounted(() => {
  console.log('unmounted')
})

function countUp() {
  count.value++
  nextTick(() => {
    console.log('nextTick')
  }) // DOMの更新後に実行。DOMの更新がない場合はすぐに実行
}

// ↓も同じ挙動
// async function countUp() {
//   count.value++
//   await nextTick()
//   console.log('nextTick')
// }
</script>

<template>
  <h2 v-bind="$attrs">CountUp</h2>
  <p>{{ count }}</p>
  <BaseIcon />
  <button @click="countUp">+</button>
</template>
