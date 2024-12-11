<script setup>
import Header from './components/Header.vue';
import CardList from './components/CardList.vue';
import Drawer from './components/Drawer.vue';
import { onMounted, ref, watch } from 'vue';
import axios from 'axios'

const items = ref([])

const sortBy = ref('')
const searchQuery = ref('')


onMounted(async () => {
  try {
    const response = await axios.get('https://78be8e41fc239fc6.mokky.dev/items')
    items.value = response.data
  } catch (error) {
    console.error(error)
  }
})

watch(sortBy, async () => {
  try {
    const response = await axios.get(`https://78be8e41fc239fc6.mokky.dev/items?title=*${searchQuery.value}*&sortBy=${sortBy.value}`)
    items.value = response.data
  } catch (error) {
    console.error(error)
  }
})

watch(searchQuery, async () => {
  try {
    const response = await axios.get(`https://78be8e41fc239fc6.mokky.dev/items?title=*${searchQuery.value}*&sortBy=${sortBy.value}`)
    items.value = response.data
  } catch (error) {
    console.error(error)
  }
})
</script>

<template>
  <!-- <Drawer /> -->
  <div class="bg-white w-4/5 m-auto rounded-xl shadow-xl mt-14">
    <Header />

    <div class="p-10">
      <div class="flex justify-between items-center mb-2">
        <h2 class="text-3xl font-bold">Все кросовоки</h2>
        <div class="flex gap-4">
          <select v-model="sortBy" class="border rounded-md outline-none py-2 px-2">
            <option value="title">По названию</option>
            <option value="price">По цене(дешевые)</option>
            <option value="-price">По цене(дорогие)</option>
          </select>
          <div class="relative">
            <img class="absolute left-3 top-3" src="/search.svg" alt="search" />
            <input v-model="searchQuery" class="border rounded-md py-2 pl-10 pr-4 outline-none focus:border-gray-400"
              placeholder="Поиск..." />
          </div>
        </div>
      </div>

      <CardList :items="items"/>
    </div>
  </div>
</template>
