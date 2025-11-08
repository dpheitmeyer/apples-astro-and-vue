<script setup>
import { ref } from 'vue'
const count = ref(0)
</script>

<template>
  <button @click="count++">This is a button and count is {{ count }}</button>
</template>

<style>
button {
  color: red;
  font-size: 0.5rem;
}
</style>