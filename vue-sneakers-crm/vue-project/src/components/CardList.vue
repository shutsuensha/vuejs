<script setup>
import Card from './Card.vue';
defineProps({
  items: Array
})
</script>

<template>
  <div class="grid grid-cols-4 gap-5" v-auto-animate="{ duration: 100 }">
    <Card v-for="item in items" :key="item.id" :item="item"/>
  </div>
</template>
