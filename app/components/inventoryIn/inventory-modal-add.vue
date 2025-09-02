<script setup lang="ts">
const open = ref(false)
</script>

<template>
  <UModal v-model:open="open" title="Add New InventoryIn" description="This is required data for adding a new item." :ui="{ footer: 'justify-end' }">
    <UButton label="Add Item" color="primary" variant="subtle" />

    <template #body>
      <Additem/>
    </template>

  </UModal>
</template>

