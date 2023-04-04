<script setup lang="ts">
import { computed, ref, watch } from 'vue'

const toggled = ref(false)
const styling = computed(() => (toggled.value ? 'filled' : ''))

let timer: number | null = null
watch(toggled, () => {
  if (timer) {
    clearTimeout(timer)
    timer = null
  }

  timer = setTimeout(() => {
    if (toggled.value) {
      toggled.value = !toggled.value
    }
  }, 500)
})
</script>

<template>
  <div class="content">
    <header>
      <h1>Behold, a useless button!</h1>
    </header>

    <main>
      <div :class="styling" role="presentation"></div>
      <button @click="toggled = !toggled" type="button">Click me</button>
    </main>
  </div>
</template>

<style scoped>
header {
  font-size: 2rem;
}
.content {
  display: grid;
  justify-items: center;
  grid-template-rows: auto 1fr;
  min-height: 100vh;
  width: 100%;
}

main button {
  background-color: white;
  border-radius: 5px;
  border: 1px solid black;
  font-size: 1.5rem;
  margin-top: 3rem;
  padding: 1rem 2rem;
}

div[role='presentation'] {
  --size: 10rem;
  border-radius: 999999px;
  background-color: red;
  height: var(--size);
  width: var(--size);
  transition: background-color 0.3s ease-in-out;
}
div[role='presentation'].filled {
  background-color: green;
}
</style>
