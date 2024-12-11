<script setup>
import Card from './Card.vue';

const onClickAdd = () => {
  alert(123)
}
defineProps({
  items: Array
})
</script>

<template>
  <div class="grid grid-cols-4 gap-5">
    <Card v-for="item in items" :key="item.id" :imageUrl="item.imageUrl" :title="item.title" :price="item.price" />
  </div>
</template>
