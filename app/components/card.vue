<script setup lang="ts">
const items = [
  {
    id: 1,
    title: "Aplikasi Menu",
    desc: "Bisa berupa web, mobile, dan desktop",
  },
  {
    id: 2,
    title: "Manajemen Hotel",
    desc: "Mempermudah dalam mengelola sistem hotel",
  },
  {
    id: 3,
    title: "Dan Lainnya",
    desc: "Masih banyak lainnya, hubungi untuk lebih lanjut",
  },
];
</script>

<template>
  <UContainer>
      <UCard v-for="item in items" :key="item.id" class="text-center">
        <template #header>
          <p class="text-xl font-bold text-orange-600">
            {{ item.title }}
          </p>
        </template>
        <p class="text-gray-600">
          {{ item.desc }}
        </p>
      </UCard>
  </UContainer>
 <UCard class="bg-[#00DC82] w-60 h-60 flex flex-col justify-center items-start p-3 rounded-lg shadow-md">
  <span class="text-base font-semibold tracking-tight text-white">Nomer Meja</span>
  <p class="mt-1 max-w-[18ch] text-white/80 text-sm">Kapasitas</p>
  <p class="mt-1 max-w-[18ch] text-white/80 text-sm">Status</p>
</UCard>
</template>
