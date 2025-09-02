<script setup lang="ts">
import { h, resolveComponent, ref, onMounted } from 'vue'
import type { TableColumn } from '@nuxt/ui'
import { useClipboard } from '@vueuse/core'

const UButton = resolveComponent('UButton')
const UBadge = resolveComponent('UBadge')
const UDropdownMenu = resolveComponent('UDropdownMenu')

const toast = useToast()
const { copy } = useClipboard()

interface Item {
  ponumber?: string;
  podate?: string;
  supplierId?: number;
  status?: string;
  totalAmount?: number;
}

const data = ref<Item[]>([])
const props = defineProps<{ items: Item[] }>();
onMounted(async () => {
  // Ganti URL sesuai endpoint API Anda
  try {
    const res = await fetch('http://localhost:5139/api/purchase')
    data.value = await res.json()
  } catch (e) {
    toast.add({
      title: 'Error',
      description: 'Failed to fetch purchase data',
      color: 'error'
    })
  }
})

const columns: TableColumn<Item>[] = [
  {
    accessorKey: 'ponumber',
    header: 'PO Number',
     cell: ({ row }) => {
      return row.getValue('ponumber')
    }  
    },
  {
    accessorKey: 'podate',
    header: 'PO Date',
    cell: ({ row }) => {
      return row.getValue('podate')
    }
  },
  {
    accessorKey: 'supplierId',
    header: 'Supplier ID'
  },
  {
    accessorKey: 'status',
    header: 'Status',
    cell: ({ row }) => {
      const color = {
        Received: 'success' as const,
        Canceled: 'error' as const,
        Pending: 'neutral' as const
      }[row.getValue('status') as string] || 'primary'
      return h(UBadge, { class: 'capitalize', variant: 'subtle', color }, () =>
        row.getValue('status')
      )
    }
  },
  {
    accessorKey: 'totalAmount',
    header: 'Total Amount',
    cell: ({ row }) => {
      return row.getValue('totalAmount')
    }
  },

]


</script>

<template>
  <UTable :data="props.items" :columns="columns" class="flex-1" />
</template>