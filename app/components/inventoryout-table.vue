<script setup lang="ts">
import { h, resolveComponent, ref, onMounted } from 'vue'
import type { TableColumn } from '@nuxt/ui'
import { useClipboard } from '@vueuse/core'

const UButton = resolveComponent('UButton')
const UBadge = resolveComponent('UBadge')
const UDropdownMenu = resolveComponent('UDropdownMenu')

const toast = useToast()
const { copy } = useClipboard()

interface Inventory {
    batchNumber?: string;
    quantity?: number;
    unitCost?: number;
}

interface Item {
    destinationType?: string;
    inventory?: Inventory;
    dateOut?: string;
    unitCost?: number;
    referenceNo?: string;
    quantityUsed?: number;
}

const data = ref<Item[]>([])
const props = defineProps<{ items: Item[] }>()

const columns: TableColumn<Item>[] = [
    {
        accessorKey: 'destinationType',
        header: 'Destination Type',
        cell: ({ row }) => row.original.destinationType ?? '-'
    },

    {
        accessorKey: 'referenceNo',
        header: 'Reference No',
        cell: ({ row }) => row.original.referenceNo ?? '-'
    },
    {
        accessorKey: 'batchNumber',
        header: 'Batch Number',
        cell: ({ row }) => row.original.inventory?.batchNumber ?? '-'
    },
    {
        accessorKey: 'unitCost',
        header: 'Unit Cost',
        cell: ({ row }) => row.original.inventory?.unitCost ?? '-'
    },
    {
        accessorKey: 'quantity',
        header: 'Quantity',
        cell: ({ row }) => row.original.inventory?.quantity ?? '-'
    },
       
    {
        accessorKey: 'dateOut',
        header: 'Date Out',
        cell: ({ row }) => row.original.dateOut ?? '-'
    }
]
</script>

<template>
    <UTable :data="props.items"  :columns="columns" class="flex-1 border rounded-lg" />
</template>
   