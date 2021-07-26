<template>
  <Flashcard />
</template>

<script>
import Flashcard from './components/Flashcard.vue'

export default {
  name: 'App',
  components: {
    Flashcard
  }
}
</script>

<style>
body {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  background-color: #54426b;
  color: #2c3e50;
}

#app {
  height: 90vh;

  display: flex;
  align-items: center;
  justify-content: center;
}
</style>
