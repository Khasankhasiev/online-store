<template>
  <div class="bg-white w-4/5 m-auto mt-14 h-screen rounded-xl shadow-xl">
    <Header></Header>
    <div>
      <div class="relative m-10 border border-slate-100 rounded-xl">
        <img class="absolute top-0 left-0" src="/like-2.svg" alt="like 2" />
        <img src="/sneakers/sneakers-1.jpg" alt="Sneakers" />
        <p>Мужские кроссовки Nike Blazer Mid Suede</p>
        <div class="flex justify between">
          <div class="flex flex-col">
            <span class="text-slate-400">Цена</span>
            <b>1205 руб.</b>
          </div>
          <img src="/plus.svg" alt="Plus" />
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import Header from '@/components/MainHeader.vue'
</script>

<style scoped></style>
