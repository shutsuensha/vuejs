<script setup>
import axios from 'axios'
const emit = defineEmits(['deleteItemBusket'])

const props = defineProps({
  item: Object
})

async function removeItemBusket() {
  try {
    await axios.patch(`https://78be8e41fc239fc6.mokky.dev/items/${props.item.id}`, {"isAdded": false})
    emit('deleteItemBusket', props.item.id)
  } catch (error) {
    console.log(error)
  }
}
</script>

<template>
  <div class="flex border items-center border-slate-200 p-4 rounded-xl gap-4">
    <img class="w-16 h-16" :src="item.imageUrl" alt="Sneaker" />
    <div class="flex flex-col justify-between">
      <p>{{ item.title }}</p>

      <div class="flex justify-between mt-2">
        <b>{{ item.price }} руб.</b>
        <img @click="removeItemBusket" class="opacity-40 hover:opacity-100 cursor-pointer transition" src="/close.svg" />
      </div>
    </div>
  </div>
</template>
