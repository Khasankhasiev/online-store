<template>
  <Drawer
    v-if="drawerIsOpen"
    :total-price="totalPrice"
    :vat-price="vatPrice"
    @create-order="createOrder"
    :is-creating-order="isCreatingOrder"
  />
  <div class="bg-white w-4/5 m-auto mt-14 rounded-xl shadow-xl">
    <Header :total-price="totalPrice" @open-drawer="openDrawer"></Header>
    <div class="p-10">
      <router-view></router-view>
    </div>
  </div>
</template>

<script setup>
import { ref, watch, provide, computed } from 'vue'
import axios from 'axios'

import Header from '@/components/TheHeader.vue'
import Drawer from '@/components/TheDrawer.vue'

// Корзина (start)
const cart = ref([])

const isCreatingOrder = ref(false)

const totalPrice = computed(() => cart.value.reduce((acc, item) => acc + item.price, 0))
const vatPrice = computed(() => Math.round((totalPrice.value * 5) / 100))

const drawerIsOpen = ref(false)

const closeDrawer = () => {
  drawerIsOpen.value = false
}

const openDrawer = () => {
  drawerIsOpen.value = true
}

const addToCart = (item) => {
  cart.value.push(item)
  item.isAdded = true
}

const removeFromCart = (item) => {
  cart.value.splice(cart.value.indexOf(item), 1)
  item.isAdded = false
}

const createOrder = async () => {
  try {
    isCreatingOrder.value = true
    const { data } = await axios.post('https://2e4a820111f9b349.mokky.dev/orders', {
      items: cart.value,
      totalPrice: totalPrice.value
    })
    cart.value = []
    return data
  } catch (err) {
    console.log(err)
  } finally {
    isCreatingOrder.value = false
  }
}

watch(
  cart,
  () => {
    localStorage.setItem('cart', JSON.stringify(cart.value))
  },
  { deep: true }
)

provide('cart', {
  cart,
  closeDrawer,
  openDrawer,
  addToCart,
  removeFromCart
})

// Корзина (END)
</script>

<style scoped></style>
