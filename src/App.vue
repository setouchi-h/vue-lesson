<script setup lang="ts">
import { ref, reactive, computed, watch, watchEffect } from 'vue'

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

const count = ref(0)
const message = ref('<h1>Password</h1><input>')
const vueUrl = ref('https://vuejs.org')
const id = ref('vue-id')

function countUp(event: MouseEvent, times: number) {
  count.value += event.clientX * times
}

const eventName = 'keyup'
const userInput = ref('')

const score = ref(2)
// const evaluation = score.value > 3 ? 'Good' : 'Bad' // 計算結果を返す
const evaluation = computed(() => {
  return score.value > 3 ? 'Good' : 'Bad' // 関数が実行されるとscore.valueを監視し、それが変化するともう一度関数を実行（score.valueを監視）。ただし、evaluationが使用されていない時は監視しない
})

watchEffect(() => {
  console.log(count.value) // computedと似ているが、副作用も含む。同期的に読み取っているreactiveのデータのみを監視する。
})

watch(count, (newVal, oldVal) => {
  // 監視したいデータを明示
  console.log(newVal, oldVal)
})

watch(
  () => {
    return count.value // 第１引数の関数はwatchEffectと同じように動作する。ただし、第２引数の関数は、第１引数の関数が返した値が変更された時(newval!=olaVal)のみ実行される。
  },
  (newVal, oldVal) => {
    // 第２引数は、1st レンダリング時は実行されない。第３引数が設定されている場合は、第１引数の関数が初めて実行される時に第２引数の関数を実行する。
    console.log('countが変更されました', newVal, oldVal)
  },
  { immediate: true } // 第３引数は、第１引数の関数が初めて実行される時に第２引数の関数を実行するかどうかを設定する。
)

const isRed = ref(true)
const isBgBlue = ref(true)
const className = ref('red')
function toggleClass() {
  isRed.value = !isRed.value
  isBgBlue.value = !isBgBlue.value
}
</script>

<template>
  <h1 class="border" :class="[className, { 'bg-blue': isBgBlue }]">Title: {{ title }}</h1>
  <h1 :style="{ color: 'red', backgroundColor: 'blue' }">Title: {{ title }}</h1>
  // "background-color"でも良い。ただし、キャメルケース推奨
  <h2>Price: ${{ price - 1 }}</h2>
  <button :disabled="false" @click="increment">Increment</button>
  <button :disabled="false" @click="price++">Increment</button>
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

  <div>{{ count }}</div>
  <div v-text="count" />
  <div v-html="message" />
  <a :id :href="vueUrl">Vue.js</a>
  <a v-bind="{ id, href: vueUrl }">Vue.js</a>

  <button @click="countUp($event, 3)">button</button>
  <button @click.prevent="count = $event.clientX">button</button>

  <input type="text" @[eventName].space.delete="count++" />

  <p>{{ userInput }}</p>
  <input v-model="userInput" type="text" />
  <button @click="userInput = 'hi'">set user input</button>

  <p>{{ score > 3 ? 'Good' : 'Bad' }}</p>
  <p>{{ evaluation }}</p>
  <p>{{ score }}</p>
  <button @click="score++">score +1</button>
  <button @click="toggleClass">toggleClass</button>
</template>
<style>
.red {
  color: red;
}
.bg-blue {
  background-color: blue;
}
.border {
  border: 1px solid black;
}
</style>
