<script setup lang="ts">
import * as z from "zod";
import type { FormSubmitEvent } from "@nuxt/ui";

const itemSchema = z.object({
  itemCode: z.string().min(2),

  itemName: z.string().min(1),
  itemType: z.string().min(1),
  unit: z.string().min(1),
  description: z.string().min(1),
});

type ItemSchema = z.output<typeof itemSchema>;

const state = reactive<Partial<ItemSchema>>({
  itemCode: "",
  itemName: "",
  itemType: undefined,
  unit: undefined,
  description: "",
});

const toast = useToast();

async function onSubmit(event: FormSubmitEvent<ItemSchema>) {
  try {
    var response = await fetch("http://localhost:5139/api/ItemMaster", {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
        Authorization: "Bearer " + localStorage.getItem("token"),
      },
      body: JSON.stringify(state),
    });
    console.log(response);
    if (!response.ok) {
      throw new Error(response + "Network response was not ok");
    }
  } catch (error) {
    console.error("Error submitting form:", error);
  }
}
toast.add({
  title: "Success",
  description: "The form has been submitted.",
  color: "success",
});
</script>

<template>
  <UForm
    :state="state"
    :schema="itemSchema"
    class="gap-4 flex flex-col w-[400px]"
    @submit="onSubmit"
  >
    <div class="grid grid-cols-2 gap-4">
      <UFormField label="Item Code" name="itemCode">
        <UInput v-model="state.itemCode" placeholder="Item Code" />
      </UFormField>
      <UFormField label="Item Name" name="itemName">
        <UInput v-model="state.itemName" placeholder="Item Name" />
      </UFormField>
      <UFormField label="Item Type" name="itemType">
        <UInput v-model="state.itemType" placeholder="Item Type" />
      </UFormField>
      <UFormField label="Unit" name="unit">
        <UInput v-model="state.unit" placeholder="Unit" />
      </UFormField>
      <UFormField label="Description" name="description" class="col-span-2">
        <UInput v-model="state.description" placeholder="Description" />
      </UFormField>
    </div>
    <div class="mt-4 flex justify-end">
      <UButton type="submit"> Submit </UButton>
    </div>
  </UForm>
</template>
