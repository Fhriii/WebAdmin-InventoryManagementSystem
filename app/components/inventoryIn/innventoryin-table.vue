<script setup lang="ts">
import { h, resolveComponent, ref, onMounted } from 'vue'
import type { TableColumn } from '@nuxt/ui'
import type { Row } from '@tanstack/table-core'
import { useClipboard } from '@vueuse/core'

const UButton = resolveComponent('UButton')
const UBadge = resolveComponent('UBadge')
const UDropdownMenu = resolveComponent('UDropdownMenu')

const toast = useToast()
const { copy } = useClipboard()

interface InvItem {
  itemCode?: string;
  itemType?: string;
  itemName?: string;
  unit?: string;
  description?: string;
}
interface Item {
  sourceType?: string;
  item?: InvItem;
  totalAmount?: number;
  unitCost?: number;
  referenceNo?: string;
  quantity?: number;
}

const props = defineProps<{ items: Item[] }>()



const columns: TableColumn<Item>[] = [
  {
    accessorKey: 'sourceType',
    header: 'Source Type',
    cell: ({ row }) => row.original.sourceType ?? '-'
  },
  {
    accessorKey: 'itemCode',
    header: 'Item Code',
    cell: ({ row }) => row.original.item?.itemCode ?? '-'
  },
  {
    accessorKey: 'itemName',
    header: 'Item Name',
    cell: ({ row }) => row.original.item?.itemName ?? '-'
  },
  {
    accessorKey: 'unit',
    header: 'Unit',
    cell: ({ row }) => row.original.item?.unit ?? '-'
  },
  {
    accessorKey: 'description',
    header: 'Description',
    cell: ({ row }) => row.original.item?.description ?? '-'
  },
  {
    accessorKey: 'totalAmount',
    header: 'Total Amount',
    cell: ({ row }) => row.original.totalAmount ?? '-'
  },
  {
    accessorKey: 'unitCost',
    header: 'Unit Cost',
    cell: ({ row }) => row.original.unitCost ?? '-'
  },
  {
    accessorKey: 'referenceNo',
    header: 'Reference No',
    cell: ({ row }) => row.original.referenceNo ?? '-'
  },
  {
    accessorKey: 'quantity',
    header: 'Quantity',
    cell: ({ row }) => row.original.quantity ?? '-'
  },
  //  {
  //   id: 'actions',
  //   cell: ({ row }) => {
  //     return h(
  //       'div',
  //       { class: 'text-right' },
  //       h(
  //         UDropdownMenu,
  //         {
  //           content: {
  //             align: 'end'
  //           },
  //           items: getRowItems(row),
  //           'aria-label': 'Actions dropdown'
  //         },
  //         () =>
  //           h(UButton, {
  //             icon: 'i-lucide-ellipsis-vertical',
  //             color: 'neutral',
  //             variant: 'ghost',
  //             class: 'ml-auto',
  //             'aria-label': 'Actions dropdown'
  //           })
  //       )
  //     )
  //   }
  // }
]


function getRowItems(row: Row<Item>) {
  return [
    {
      type: 'label',
      label: 'Actions'
    },
    {
      label: 'Copy payment ID',
      onSelect() {

        toast.add({
          title: 'Payment ID copied to clipboard!',
          color: 'success',
          icon: 'i-lucide-circle-check'
        })
      }
    },
    {
      type: 'separator'
    },
    {
      label: 'View customer'
    },
    {
      label: 'View payment details'
    }
  ]
}
</script>

<template>
  <InventoryInInventoryModalAdd />
  <UTable :data="props.items" :columns="columns" class="flex-1" />
</template>