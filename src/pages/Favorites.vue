<template>
  <h2 class="text-3xl font-bold mb-8">Мои закладки</h2>

  <CardList :items="favorites" is-favorites />
</template>

<script setup>
import axios from 'axios'
import { onMounted, ref } from 'vue'

import CardList from '@/components/CatalogCardList.vue'

const favorites = ref([])

onMounted(async () => {
  try {
    const { data } = await axios.get(
      'https://2e4a820111f9b349.mokky.dev/favorites?_relations=items'
    )
    favorites.value = data.map((obj) => obj.item)
  } catch (err) {
    console.log(err)
  }
})
</script>
