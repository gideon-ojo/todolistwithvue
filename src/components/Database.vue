<template>
     name: {{ name }}
     department: {{ department }}
     salary: {{ salary }}
     position: {{ position }}
</template>
<script setup>
  defineProps({
    name: String,
    department: String,
    salary: Number,
    position: Number
  })
</script>