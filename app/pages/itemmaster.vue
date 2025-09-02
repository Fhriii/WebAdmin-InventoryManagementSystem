<script setup lang="ts">
import Table from '../components/table.vue';
import Navigation from '../components/navigation.vue';
import Card from '../components/card.vue';


const items = ref([])
async function fetchItems() {
  const response = await fetch("http://localhost:5139/api/ItemMaster", {  })
  const data = await response.json()
  items.value = data
}
fetchItems()

</script>

<template>

    <div class>
        <h1 class="text-2xl font-bold mb-4 text-white ">Item Master</h1><br/>
        <div class="flex justify-end mb-4 mr-5">
            <ModalAddItem />
        </div>
        <Table :items="items" />
    </div>

</template>

