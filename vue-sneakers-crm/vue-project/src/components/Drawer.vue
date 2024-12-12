<script setup>
import DrawerHeader from './DrawerHeader.vue'
import CartItemList from './CartItemList.vue';
import { ref, watch } from 'vue'

const emit = defineEmits(['response', 'deleteItemBusket'])

const props = defineProps({
  basketItems: Array
})


const totalPrice = ref(0)
const nalogPrice = ref(0)

const order = ref(false)

watch(
  () => props.basketItems,
  (newBasketItems) => {
    totalPrice.value = newBasketItems.reduce((sum, item) => sum + item.price, 0);
    nalogPrice.value = totalPrice.value - (totalPrice.value * 0.05)
  },
  { deep: true } 
);

function makeOrder() {
  order.value = true
}

</script>

<template>
  <div @click="emit('response', false)" class="fixed top-0 left-0 h-full w-full bg-black z-10 opacity-70"></div>
  <div class="bg-white w-96 h-full fixed right-0 top-0 z-20 p-8">
    <DrawerHeader @response="(childClose) => emit('response', childClose)" />

    <CartItemList @deleteItemBusket="(itemBusketId) => emit('deleteItemBusket', itemBusketId)" v-if="props.basketItems.length !== 0 && order === false" :basketItems="props.basketItems"/>
    <div v-if="props.basketItems.length !== 0 && order === false" class="flex flex-col gap-4 my-7">
      <div class="flex gap-2">
        <span>Итого:</span>
        <div class="flex-1 border-b border-dashed"></div>
        <b>{{ totalPrice }} руб.</b>
      </div>

      <div class="flex gap-2">
        <span>Налог 5%:</span>
        <div class="flex-1 border-b border-dashed"></div>
        <b>{{ nalogPrice }} руб.</b>
      </div>

      <button @click="makeOrder" class="mt-4 bg-lime-500 w-full rounded-xl py-3 text-white hover:bg-lime-600 active:bg-lime-700 disabled:bg-slate-300 cursor-pointer">Оформить
        заказ</button>
    </div>
    <div v-if="props.basketItems.length === 0 && order === false">
      Тут ничего нет
    </div>
    <div v-if="order">
      Заказ оформен
    </div>
  </div>
</template>
