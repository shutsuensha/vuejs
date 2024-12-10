<script setup>
import Card from './Card.vue';

const onClickAdd = () => {
  alert(123)
}
</script>

<template>
  <div class="grid grid-cols-4 gap-5">
    <Card imageUrl="/sneakers/sneakers-1.jpg" title="Мужские кросовки Nike Blazer Mid Suede" :price="5000"
      :isAdded="false" :isFavorite="false" :onClickAdd="onClickAdd"/>
  </div>
</template>
