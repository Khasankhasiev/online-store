<template>
  <div class="flex flex-col flex-1 gap-4 justify-between" v-auto-animate>
    <CartItem
      v-for="item in cart"
      :key="item.id"
      :title="item.title"
      :image-url="item.imageUrl"
      :price="item.price"
      @on-click-remove="() => removeFromCart(item)"
    />
  </div>
</template>

<script setup>
import CartItem from '@/components/CartItem.vue'
import { inject } from 'vue'

const { cart, removeFromCart } = inject('cart')
</script>

<style scoped></style>
