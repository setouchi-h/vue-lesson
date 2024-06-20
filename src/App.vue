<script setup>
import { resolveModuleNameFromCache } from 'typescript'
import { ref, reactive } from 'vue'

const title = ref('Vue.js Course')
let price = ref(9.99)
const info = ref({
  students: 100,
  rating: 4.5
}) // refの引数にオブジェクトが渡された場合、内部的にはreactiveが使われる。reactiveよりrefを公式は推奨
const instructor = reactive({
  name: 'John',
  age: 30,
  sns: { twitter: '@john', facebook: '@john' },
  email: ref('john@example.com')
})
console.log(instructor.email) // refの場合は、.valueは不要
instructor.bio = 'John is a web developer'
const items = reactive([ref(1), ref(2), ref(3)])
console.log(items[0].value) // refの配列の場合は、.valueが必要

const courseInfo = {
  section: ref(10),
  language: ref('English')
}

function increment() {
  price.value += 1
  instructor.age += 1
}
</script>

<template>
  <h1>Title: {{ title }}</h1>
  <h2>Price: ${{ price - 1 }}</h2>
  <button @click="increment">Increment</button>
  <h2>Students: {{ info.students }}</h2>
  <h2>Rating: {{ info.rating }}</h2>
  <h2>Instructor: {{ instructor.name }}</h2>
  <h2>Age: {{ instructor.age }}</h2>
  <h2>Bio: {{ instructor.bio }}</h2>
  <h2>Twitter: {{ instructor.sns.twitter }}</h2>
  <h2>Facebook: {{ instructor.sns.facebook }}</h2>
  <h2>Email: {{ instructor.email }}</h2>
  <h2>Section: {{ courseInfo.section.value + 1 }}</h2>
  <h2>Language: {{ courseInfo.language }}</h2>
</template>
