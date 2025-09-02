<template lang="">
  <!-- <div style="display: flex; min-height: 100vh;" orientation="horizontal"> -->
  <!-- <div style="width: 220px;  padding: 20px 0;">
        <Navigation />
    </div> -->
  <div>
    <h1 class="text-2xl font-bold mb-4 text-white">Request Order</h1>
    <br />
    <modalAddRequest class="mb-4" />
    <requestorderTable
      :items="items"
    class="border rounded-lg"
        :onRefresh="fetchItems"  
    />
  </div>
</template>
<script setup>
import requestorderTable from "~/components/requestorder-table.vue";
import modalAddRequest from "~/components/modal-cancel-request.vue";
const items = ref([]);
async function fetchItems() {
  const response = await fetch("http://localhost:5139/api/RequestOrder", {
    method: "GET",
    headers: {
      "Content-Type": "application/json",
      Authorization: "Bearer " + localStorage.getItem("token"),
    },
  });
  const data = await response.json();
  items.value = data;
}
fetchItems();
</script>
<style lang=""></style>
