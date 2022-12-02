<script setup>
import { ref, onMounted } from 'vue'

const joke = ref({})
const show = ref(false)

onMounted(() => loadJoke())

const loadJoke = async () => {
  show.value = false
  joke.value = await (await fetch('https://v2.jokeapi.dev/joke/christmas')).json()
}
</script>

<template>
  <div class="w-full h-full flex flex-col gap-4 justify-center items-center">
    <span class="text-3xl">Joke Generator</span>
    <p data-qa="setup">{{ joke.setup }}</p>
    <template v-if="show">
      <p>{{ joke.delivery }}</p>
      <button @click="loadJoke">Another</button>
    </template>
    <template v-else>
      <p>&nbsp;</p>
      <button @click="show = true">Tell Me!</button>
    </template>
  </div>
</template>

<style scoped>
button {
  border: 1px solid black;
  padding: 2px 5px;
}
</style>
