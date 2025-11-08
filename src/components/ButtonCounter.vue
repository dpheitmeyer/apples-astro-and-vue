<script setup>
import { ref } from 'vue'
const count = ref(0)
</script>

<template>
  <button @click="count++">This is a button and count is {{ count }}</button>
</template>

<style>
button {
  color: orange;
  background-color: black;
  padding: 1rem;
  border-radius: 1rem;
  font-size: 1.5rem;
}
</style>
