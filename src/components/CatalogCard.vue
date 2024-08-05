<template>
  <a
    href="#"
    class="relative bg-white border border-slate-100 rounded-3xl p-8 cursor-pointer hover:-translate-y-2 hover:shadow-xl transition"
  >
    <button @click="onClickFavorite" type="button" class="absolute top-8 left-8">
      <img v-if="onClickFavorite" :src="!isFavorite ? '/like-1.svg' : '/like-2.svg'" alt="like 2" />
    </button>

    <img :src="imageUrl" alt="Sneakers" />
    <p class="mt-2">{{ title }}</p>
    <div class="flex justify-between mt-5">
      <div class="flex flex-col">
        <span class="text-slate-400">Цена</span>
        <b>{{ price }} руб.</b>
      </div>
      <button type="button" @click.prevent="onClickAdd">
        <img v-if="onClickAdd" :src="!isAdded ? '/plus.svg' : '/checked.svg'" alt="Plus" />
      </button>
    </div>
  </a>
</template>

<script setup>
defineProps({
  id: Number,
  imageUrl: String,
  title: String,
  price: Number,
  isFavorite: Boolean,
  isAdded: Boolean,
  onClickAdd: Function,
  onClickFavorite: Function
})
</script>

<style scoped></style>
