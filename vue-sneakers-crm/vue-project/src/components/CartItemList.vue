<script setup>
import CartItem from './CartItem.vue';

const emit = defineEmits(['deleteItemBusket'])
defineProps({
  basketItems: Array
})
</script>

<template>
	<div class="flex flex-col gap-4">
		<CartItem v-auto-animate="{ duration: 100 }" @deleteItemBusket="(itemBusketId) => emit('deleteItemBusket', itemBusketId)" v-for="item in basketItems" :key="item.id" :item="item"/>
	</div>
</template>