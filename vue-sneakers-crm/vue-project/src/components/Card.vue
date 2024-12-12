<script setup>
import axios from 'axios'


const props = defineProps({
  item: Object
})

async function onClickFavorite() {
  try {
    props.item.isFavorite = !props.item.isFavorite
    await axios.patch(`https://78be8e41fc239fc6.mokky.dev/items/${props.item.id}`, {"isFavorite": props.item.isFavorite})
  } catch (error) {
    console.log(error)
  }
}

async function onClickAdd() {
  try {
    props.item.isAdded = !props.item.isAdded
    await axios.patch(`https://78be8e41fc239fc6.mokky.dev/items/${props.item.id}`, {"isAdded": props.item.isAdded})
  } catch (error) {
    console.log(error)
  }
}
</script>

<template>
  <div
    class="relative bg-white border border-slate-100 rounded-3xl p-8 cursor-pointer transition hover:-translate-y-2 hover:shadow-xl">
    <img @click="onClickFavorite" v-if="item.isFavorite" src="/like-2.svg" alt="like 1" class="absolute top-0 left-0" />
    <img @click="onClickFavorite" v-else src="/like-1.svg" alt="like 1" class="absolute top-0 left-0" />
    <img :src="item.imageUrl" alt="Sneaker" />

    <p class="mt-2">{{ item.title }}</p>

    <div class="flex justify-between mt-5">
      <div class="flex flex-col">
        <span class="text-slate-400">Цена:</span>
        <b> {{ item.price }} руб.</b>
      </div>
      <img v-if="item.isAdded" src="/checked.svg" alt="Checked" @click="onClickAdd" />
      <img v-else src="/plus.svg" alt="Plus" @click="onClickAdd" />
    </div>
  </div>
</template>
