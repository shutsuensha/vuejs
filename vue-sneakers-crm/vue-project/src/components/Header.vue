<script setup>
const emit = defineEmits(['response'])

async function openBusketFunction() {
  emit('response', true)
}

defineProps({
  totalPrice: Number
})
</script>

<template>
  <header class="flex justify-between border-b border-slate-100 px-10 py-8">
    <div class="flex items-center gap-4">
      <img src="/logo.png" alt="Logo" class="w-10" />
      <div>
        <h2 class="text-xl font-bold uppercase">Vue Sneakers</h2>
        <p class="text-slate-400">Магазин лучших кросовок</p>
      </div>
    </div>

    <ul class="flex items-center gap-10">
      <li @click="openBusketFunction" class="flex items-center cursor-pointer gap-3 text-slate-500 hover:text-black">
        <img src="/cart.svg" alt="Cart" />
        <b v-if="totalPrice !== 0">{{ totalPrice }} руб.</b>
      </li>

      <li class="flex items-center cursor-pointer gap-3 text-slate-500 hover:text-black">
        <img src="/heart.svg" alt="Heart" />
        <span>Закладки</span>
      </li>

      <li class="flex items-center cursor-pointer gap-3 text-slate-500 hover:text-black">
        <img src="/profile.svg" alt="Profile" />
        <span>Profile.</span>
      </li>
    </ul>
  </header>
</template>
