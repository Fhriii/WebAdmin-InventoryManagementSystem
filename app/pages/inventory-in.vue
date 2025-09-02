<template lang="">
  
<!-- <div style="display: flex; min-height: 100vh;" orientation="horizontal"> -->
    <!-- <div style="width: 220px;  padding: 20px 0;">
        <Navigation />
    </div> -->
    <div class="ml-1.5 mr-1">
        <h1 class="text-2xl font-bold mb-4 text-white ">Inventory In</h1><br/>
        <innventoryinTable :items="items" class="border" style="border-radius: 8px;" />
    </div>

</template>
<script setup>

import innventoryinTable from '~/components/inventoryIn/innventoryin-table.vue'
const items = ref([])
async function fetchItems() {
  const response = await fetch("http://localhost:5139/api/Inventory/InventoryIn", {
     method: 'GET',
     headers: {
       'Content-Type': 'application/json', 'Authorization': 'Bearer ' + localStorage.getItem('token')
     }
   })
  const data = await response.json()
  items.value = data
}
fetchItems()

</script>
<style lang="">
    
</style>