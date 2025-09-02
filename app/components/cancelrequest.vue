<script setup lang="ts">
import * as z from "zod";
import type { FormSubmitEvent } from "@nuxt/ui";
import { ref, reactive, onMounted, watch } from "vue";

const emit = defineEmits(['submitted'])

const itemSchema = z.object({
  status: z.string().min(2, { message: "Customer Name is required" }),
  requestCode: z.string().min(2, { message: "Item Code is required" }),
});

type ItemSchema = z.output<typeof itemSchema>;

const props = defineProps<{
  status: string;
  requestCode: string;
}>();

const state = reactive<ItemSchema>({
  status: props.status || "",
  requestCode: props.requestCode || "",
});

const toast = useToast();
const items = ref<string[]>([]);
const loading = ref(false);

// Fetch item codes for select menu
async function fetchItems() {
  loading.value = true;
  try {
    const response = await fetch("http://localhost:5139/api/ItemMaster", {
      method: "GET",
      headers: {
        "Content-Type": "application/json",
        Authorization: "Bearer " + localStorage.getItem("token"),
      },
    });
    const data = await response.json();
    items.value = Array.isArray(data) ? data.map((item: any) => item.requestCode) : [];
    // Set default requestCode jika props ada dan ada di list
    if (props.requestCode && items.value.includes(props.requestCode)) {
      state.requestCode = props.requestCode;
    }
  } catch (error) {
    toast.add({
      title: "Error",
      description: "Failed to fetch item codes.",
      color: "error",
    });
  } finally {
    loading.value = false;
  }
}
onMounted(fetchItems);
var status = ref<string[]>([
  'Completed',
  'Canceled',
  'Pending',
  'InProduction'
]);
watch(
  () => state.requestCode,
  (val) => {
    if (!items.value.includes(val)) state.requestCode = "";
  }
);

async function onSubmit(event: FormSubmitEvent<ItemSchema>) {
  try {
    if(state.requestCode === "Request Code") {
      toast.add({
        title: "Error",
        description: "Please select a valid Request Code.",
        color: "error",
      });
      return;
    }
    if(state.status == "Completed") {
      toast.add({
        title: "Error",
        description: "Please select a valid Status.",
        color: "error",
      });
      return;
    }
    var reqcode = encodeURIComponent(state.requestCode)
    const response = await fetch(`http://localhost:5139/api/RequestOrder/UpdateStatusRequest/${reqcode}`, {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
        Authorization: "Bearer " + localStorage.getItem("token"),
      },
      body: JSON.stringify({ status: state.status }), // <-- harus objek
    });
    console.log(response);
    
    if (!response.ok) throw new Error("Network response was not ok");
    toast.add({
      title: "Success",
      description: "The form has been submitted.",
      color: "success",
    });
        emit('submitted') 

  } catch (error) {
    toast.add({
      title: "Error",
      description: "Error submitting form.",
      color: "error",
    });
    console.error("Error submitting form:", error);
  }
}
</script>
<template>
  <UForm
    :state="state"
    :schema="itemSchema"
    class="gap-4 flex flex-col w-[400px]"
    @submit="onSubmit"
  >
    <UFormField label="Request Code" name="requestCode">
      <UInput
      v-model="state.requestCode"
      placeholder="Item Code"
      class="w-full"
      disabled
      />
    </UFormField>
    <UFormField label="Status" name="status">
        <USelectMenu
          v-model="state.status"
          :items="status"
          placeholder="Select Status"
          class="w-48"
          :loading="loading"
        />
    </UFormField>

    <div class="mt-4 flex justify-end">
      <UButton type="submit">Submit</UButton>
    </div>
  </UForm>
</template>