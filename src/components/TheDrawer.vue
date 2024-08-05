<template>
  <div @click="closeDrawer" class="fixed top-0 left-0 z-10 w-full h-full bg-black opacity-70"></div>

  <div class="fixed top-0 right-0 z-20 w-96 h-full bg-white p-8">
    <DrawerHead />

    <div v-if="!totalPrice || orderId" class="flex h-full items-center">
      <InfoBlock
        v-if="!totalPrice && !orderId"
        title="Корзина пустая"
        description="Добавьте хотя бы одну пару кроссовок, чтобы сделать заказ"
        imageUrl="/package-icon.png"
      />
      <InfoBlock
        v-if="orderId"
        title="Заказ оформлен!"
        :description="`Ваш заказ №${orderId} скоро будет передан курьерской доставке`"
        imageUrl="/order-success-icon.png"
      />
    </div>

    <div v-else>
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
          :disabled="buttonDisabled"
          @click="createOrder"
          class="mt-4 bg-lime-500 w-full rounded-xl py-3 text-white hover:bg-lime-600 transition active:bg-lime-700 disabled:bg-slate-300 cursor-pointer"
        >
          Оформить заказ
        </button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { computed, inject, ref } from 'vue'
import axios from 'axios'

import DrawerHead from '@/components/DrawerHead.vue'
import DrawerCartList from '@/components/CartList.vue'
import InfoBlock from '@/components/InfoBlock.vue'

const props = defineProps({
  totalPrice: Number,
  vatPrice: Number
})

const { closeDrawer, cart } = inject('cart')

const isCreatingOrder = ref(false)
const orderId = ref(null)

const cartIsEmpty = computed(() => cart.value.length === 0)
const buttonDisabled = computed(() => isCreatingOrder.value || cartIsEmpty.value)

const createOrder = async () => {
  try {
    isCreatingOrder.value = true
    const { data } = await axios.post('https://2e4a820111f9b349.mokky.dev/orders', {
      items: cart.value,
      totalPrice: props.totalPrice
    })
    cart.value = []
    orderId.value = data.id
  } catch (err) {
    console.log(err)
  } finally {
    isCreatingOrder.value = false
  }
}
</script>
