<template>
  <div @click="closeDrawer" class="fixed top-0 left-0 z-10 w-full h-full bg-black opacity-70"></div>

  <div class="fixed top-0 right-0 z-20 w-96 h-full bg-white p-8">
    <DrawerHead />
    <DrawerCartList />

    <div class="flex flex-col gap-4 mt-7">
      <div class="flex gap-2">
        <span>Итого:</span>
        <div class="flex-1 border-b border-dashed"></div>
        <b>{{ totalPrice }} ₽</b>
      </div>

      <div class="flex gap-2">
        <span>Налог 5%:</span>
        <div class="flex-1 border-b border-dashed"></div>
        <b>{{ vatPrice }} ₽</b>
      </div>

      <button
        disabled
        class="mt-4 bg-lime-500 w-full rounded-xl py-3 text-white hover:bg-lime-600 transition active:bg-lime-700 disabled:bg-slate-300 cursor-pointer"
      >
        Оформить заказ
      </button>
    </div>
  </div>
</template>

<script setup>
import DrawerHead from '@/components/DrawerHead.vue'
import DrawerCartList from '@/components/DrawerCartList.vue'
import { inject } from 'vue'

defineProps({
  totalPrice: Number,
  vatPrice: Number
})

const { closeDrawer } = inject('cart')
</script>
