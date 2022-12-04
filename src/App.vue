<template>
  <div class='w-full h-full flex justify-center items-center'>
    <div class='max-w-xs w-full flex flex-col'>
      <template v-if='!isLoading'>
        <div class='w-3/4 p-4 rounded-2xl bg-teal-800 text-white self-start mb-4'>{{ joke }}</div>
        <div class='w-3/4 p-4 rounded-2xl bg-red-800 text-white self-end' v-if='showAnswer'>{{ jokeAnswer }}</div>
        <button v-if='!showAnswer' @click='showAnswer = true'
                class='bg-green col-span-1 rounded-lg py-2 hover:opacity-90 w-full mx-auto mt-4'>
          Tell Me!
        </button>
        <button v-if='showAnswer' @click='getJoke'
                class='bg-green col-span-1 rounded-lg py-2 hover:opacity-90 w-full mx-auto mt-4'>
          Another
        </button>
      </template>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const joke = ref(null)
const jokeAnswer = ref(null)
const showAnswer = ref(false)
const isLoading = ref(true)

const getJoke = () => {
  showAnswer.value = false
  joke.value = null
  jokeAnswer.value = null
  fetch('https://v2.jokeapi.dev/joke/christmas').then(res => res.json()).then(data => {
    joke.value = data.setup
    jokeAnswer.value = data.delivery
  }).finally(() => {
    isLoading.value = false
  })
}
getJoke()
</script>
