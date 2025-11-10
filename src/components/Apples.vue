<script setup>
import { ref, onMounted } from 'vue'

const apples = ref(null)
const loading = ref(true)
const error = ref(null)

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

  /* put in some error catching with the "try, catch, finally" approach
  https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/try...catch
  */
  try {
    const response = await fetch(url)
    if (!response.ok) throw new Error('Failed to get data')
    const appleData = await response.json()
    apples.value = appleData.apples
  } catch (err) {
    error.value = err.message
  } finally {
    loading.value = false
    console.log(apples.value)
  }
})
</script>

<template>
  <div v-if="loading" class="loading">
    <div class="loading-icon">◌</div>
    <div class="loading-message">loading weather...</div>
  </div>
  <div v-else-if="error" class="error">
    <div class="error-icon">⚠️</div>
    <div class="error-message">{{ error }}</div>
  </div>
  <div v-else-if="apples">
    <h1>Apples</h1>
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
  </div>
</template>

<style>
.loading {
  text-align: center;
  color: #3a3a3a;
}
.loading,
.error {
  padding: 1rem;

  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 1.5rem;
}
.error {
    border: 5px solid red;
  border-radius: 1rem;
  background-color: rgb(255, 230, 230);
}
.error-icon, .loading-icon {
  font-size: 3rem;
  padding-right: 1rem;
}
</style>
