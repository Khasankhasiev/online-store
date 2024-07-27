<template>
  <div class="grid grid-cols-4 gap-5">
    <Card
      v-for="item in items"
      :key="item.id"
      :title="item.title"
      :image-url="item.imageUrl"
      :price="item.price"
      :onclickAdd="onClickAdd"
    />
  </div>
</template>

<script setup>
import Card from '@/components/CatalogCard.vue'

defineProps({
  items: Array
})

const onClickAdd = () => {
  console.log('Добавлено')
}
</script>

<style scoped></style>
