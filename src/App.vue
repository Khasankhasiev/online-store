<template>
  <Drawer />
  <div class="bg-white w-4/5 m-auto mt-14 rounded-xl shadow-xl">
    <Header></Header>
    <div class="p-10">
      <h2 class="text-3xl font-bold mb-8">Все кроссовки</h2>
      <CardList />
    </div>
  </div>
</template>

<script setup>
import Header from '@/components/MainHeader.vue'
import CardList from '@/components/CatalogCardList.vue'
import Drawer from '@/components/CatalogDrawer.vue'
</script>

<style scoped></style>
