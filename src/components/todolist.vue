<template>
  <div class="container">
   <input type="text">
  </div>
</template>

<script setup>
 const API_KEY = 'https://x/RKKJcfNCoznoEajqZsTDdH9GHDSYCe6e6+gOtfpzFU9N7P'
 async function getData() {
  const responce = await fetch(API_KEY)
  const data = await responce.json()
  console.log(data)
 }
 getData();
</script>

<style scoped>

</style>