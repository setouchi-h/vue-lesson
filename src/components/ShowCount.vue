<script setup>
// const props = defineProps(['foo', 'bar'])
const props = defineProps({
  totalScore: {
    type: Number,
    required: false,
    default: 0,
    validator(value) {
      return value >= 0
    }
  },
  bar: {
    type: [Number, String],
    required: false,
    default: function () {
      return [] // オブジェクト、配列の場合は関数の返り値として設定する必要がある
    }
  },
  bool: Boolean
})
console.log(props.foo) // reactiveなデータ、readonly
</script>

<template>
  <p>count: {{ totalScore }}</p>
  <p>{{ bar }}</p>
  <p>{{ bool }}</p>
</template>
