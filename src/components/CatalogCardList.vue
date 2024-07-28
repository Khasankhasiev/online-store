<template>
  <div class="grid grid-cols-4 gap-5">
    <Card
      v-for="item in items"
      :key="item.id"
      :title="item.title"
      :image-url="item.imageUrl"
      :price="item.price"
      :id="item.id"
      :isFavorite="item.isFavorite"
      :onClickFavorite="() => emit('addToFavorite', item)"
    />
  </div>
</template>

<script setup>
import Card from '@/components/CatalogCard.vue'

defineProps({
  items: Array
})

const emit = defineEmits(['addToFavorite'])
</script>

<style scoped></style>
