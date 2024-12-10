<script setup>
const props = defineProps({
  title: String,
  imageUrl: String,
  price: Number,
  isFavorite: Boolean,
  isAdded: Boolean,
  onClickAdd: Function,
  onClickFavorite: Function
})

function toogleAddRemove() {

}
</script>

<template>
  <div
    class="relative bg-white border border-slate-100 rounded-3xl p-8 cursor-pointer transition hover:-translate-y-2 hover:shadow-xl">
    <img @click="onClickFavorite" v-if="isFavorite" src="/like-2.svg" alt="like 1" class="absolute top-0 left-0" />
    <img @click="onClickFavorite" v-else src="/like-1.svg" alt="like 1" class="absolute top-0 left-0" />
    <img :src="imageUrl" alt="Sneaker" />

    <p class="mt-2">{{ title }}</p>

    <div class="flex justify-between mt-5">
      <div class="flex flex-col">
        <span class="text-slate-400">Цена:</span>
        <b> {{ price }} руб.</b>
      </div>
      <img v-if="isAdded" src="/checked.svg" alt="Checked" @click="onClickAdd" />
      <img v-else src="/plus.svg" alt="Plus" @click="onClickAdd" />
    </div>
  </div>
</template>
