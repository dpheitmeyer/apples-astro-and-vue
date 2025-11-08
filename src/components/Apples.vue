<script setup>
import { ref, onMounted } from 'vue'

const apples = ref(null)

defineProps({
  now: { type: Boolean, default: true },
  soon: { type: Boolean, default: false },
  done: { type: Boolean, default: false },
})
onMounted(async () => {
  console.log(`the component is now mounted.`)

  /* fetch apple info at 
     https://cscie12.dce.harvard.edu/apples-pyo.php
     */
  const url = 'https://cscie12.dce.harvard.edu/apples-pyo.php'
  const response = await fetch(url)
  const appleData = await response.json()
  apples.value = appleData.apples
  console.log(apples.value)
})
</script>

<template>
  <div v-if="now">
    <h2>Picking Now</h2>
    <ul>
      <li v-for="(variety, index) in apples?.picking_now" :key="index">{{ variety }}</li>
    </ul>
  </div>

  <div v-if="soon">
    <h2>Picking Soon</h2>
    <ul>
      <li v-for="(variety, index) in apples?.picking_soon" :key="index">{{ variety }}</li>
    </ul>
  </div>

  <div v-if="done">
    <h2>Done for the Season</h2>
    <ul>
      <li v-for="(variety, index) in apples?.picking_done" :key="index">{{ variety }}</li>
    </ul>
  </div>
</template>

<style></style>
