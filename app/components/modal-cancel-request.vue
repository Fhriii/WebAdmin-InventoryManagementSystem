<script setup lang="ts">
import { ref, watch } from "vue";
import Addrequest from "./cancelrequest.vue";
const props = defineProps<{
  open: boolean;
  status: string;
  requestCode: string;
}>();
const emit = defineEmits(["update:open","submitted"]);
const openRef = ref(props.open);
watch(
  () => props.open,
  (val) => {
    openRef.value = val;
  }
);
watch(openRef, (val) => {
  emit("update:open", val);
});
</script>

<template>
  <UModal
    v-model:open="openRef"
    title="Add New Request Order"
    description="This is required data for adding a new request order."
    :ui="{ footer: 'justify-end' }"
  >
    <template #body>
      <cancelrequest
        :status="props.status"
        :requestCode="props.requestCode"
        @submitted="emit('submitted')"
      />
    </template>
  </UModal>
</template>
