<script setup lang="ts">
interface Item {
  itemCode?: string;
  itemName?: string;
  itemType?: string;
  unit?: string;
  description?: string;
  // tambahkan field lain sesuai kebutuhan
}
const props = defineProps<{ items: Item[] }>();
</script>

<template>
  <!-- <UTable :data="props.items" class="flex-1 mb-6" /> -->
  <div
    class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-4" orientation="vertical"
  >
    <UCard
      v-for="(item, index) in props.items"
      :key="index"
      class="bg-[#00834c] w-60 h-30 flex flex-col justify-center items-start p-3 rounded-lg shadow-md"
    >
      <span class="text-base font-semibold tracking-tight text-white">{{
        item.itemCode
      }}</span>
      <p class="mt-1 max-w-[40ch] text-white/80 text-sm">{{ item.itemName }}</p>
      <p class="mt-1 max-w-[18ch] text-white/80 text-sm">{{ item.itemType }}</p>
      <p class="mt-1 max-w-[40ch] text-white/80 text-sm">
        {{ item.description }}
      </p>
    </UCard>
  </div>
</template>
