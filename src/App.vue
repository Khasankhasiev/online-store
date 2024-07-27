<template>
  <Drawer v-if="false" />
  <div class="bg-white w-4/5 m-auto mt-14 rounded-xl shadow-xl">
    <Header></Header>
    <div class="p-10">
      <div class="flex justify-between items-center">
        <h2 class="text-3xl font-bold mb-8">Все кроссовки</h2>

        <div class="flex gap-4">
          <select name="" id="" class="py-2 px-3 border rounded-md outline-none">
            <option value="">По названию</option>
            <option value="">По цене (дешевые)</option>
            <option value="">По цене (дорогие)</option>
          </select>

          <div class="relative">
            <img class="absolute left-4 top-3" src="/search.svg" />
            <input
              class="border rounded-md py-2 pl-12 pr-4 outline-none focus:border-gray-400"
              type="text"
              placeholder="Поиск..."
            />
          </div>
        </div>
      </div>
      <div class="mt-10">
        <CardList :items="items" />
      </div>
    </div>
  </div>
</template>

<script setup>
import { onMounted, ref } from 'vue'
import axios from 'axios'

import Header from '@/components/MainHeader.vue'
import CardList from '@/components/CatalogCardList.vue'
import Drawer from '@/components/CatalogDrawer.vue'

const items = ref([])

onMounted(async () => {
  // fetch('https://2e4a820111f9b349.mokky.dev/items')
  //   .then((res) => res.json())
  //   .then((data) => {
  //     console.log(data)
  //   })
  try {
    const { data } = await axios.get('https://2e4a820111f9b349.mokky.dev/items')
    items.value = data
  } catch (err) {
    console.log(err)
  }
})
</script>

<style scoped></style>
