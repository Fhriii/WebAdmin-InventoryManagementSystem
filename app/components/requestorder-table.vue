<script setup lang="ts">
import { h, resolveComponent, ref } from 'vue'
import type { TableColumn } from '@nuxt/ui'
import { useClipboard } from '@vueuse/core'

const UButton = resolveComponent('UButton')
const UBadge = resolveComponent('UBadge')
const UDropdownMenu = resolveComponent('UDropdownMenu')
const selectedStatus = ref('')
const selectedRequestCode = ref('')
const toast = useToast()
const { copy } = useClipboard()

interface Item {
    itemCode?: string;
    itemName?: string;
}

interface RequestOrder {
    requestNumber?: string;
    customerName?: string;
    customerPhone?: string;
    status?: string;
    quantity?: number;
    item?: Item;
}

const props = defineProps<{
  items: RequestOrder[],
  onRefresh: () => void
}>()
const isModalOpen = ref(false)

const columns: TableColumn<RequestOrder>[] = [
   {
    id: 'expand',
    cell: ({ row }) =>
      h(UButton, {
        color: 'neutral',
        variant: 'ghost',
        icon: 'i-lucide-chevron-down',
        square: true,
        'aria-label': 'Expand',
        ui: {
          leadingIcon: [
            'transition-transform',
            row.getIsExpanded() ? 'duration-200 rotate-180' : ''
          ]
        },
        onClick: () => row.toggleExpanded()
      })
  },
    {
        accessorKey: 'requestNumber',
        header: 'Request Number',
        cell: ({ row }) => row.original.requestNumber ?? '-'
    },
    {
        accessorKey: 'customerName',
        header: 'Customer Name',
        cell: ({ row }) => row.original.customerName ?? '-'
    },
    {
        accessorKey: 'customerPhone',
        header: 'Customer Phone',
        cell: ({ row }) => row.original.customerPhone ?? '-'
    },
    {
        accessorKey: 'status',
        header: 'Status',
        cell: ({ row }) => row.original.status ?? '-'
    },
      {
    id: 'actions',
    cell: ({ row }) => {
      return h(
        'div',
        { class: 'text-right' },
        h(
          UDropdownMenu,
          {
            content: {
              align: 'end'
            },
            items: getRowItems(row),
            'aria-label': 'Actions dropdown'
          },
          () =>
            h(UButton, {
              icon: 'i-lucide-ellipsis-vertical',
              color: 'neutral',
              variant: 'ghost',
              class: 'ml-auto',
              'aria-label': 'Actions dropdown'
            })
        )
      )
    }
}
]

function getRowItems(row: any) {
  return [
    {
      type: 'label',
      label: 'Actions'
    },
    {
      label: 'Edit status',
      onSelect() {
        openModal(row.original)
        toast.add({
          title: 'Payment ID copied to clipboard!',
          color: 'success',
          icon: 'i-lucide-circle-check'
        })
      }
    },
   
  ]
}
function handleSubmitted() {
  isModalOpen.value = false
  props.onRefresh && props.onRefresh() // panggil fetchItems dari parent
}
function openModal(row: RequestOrder) {
  selectedStatus.value = row.status ?? ''
  selectedRequestCode.value = row.requestNumber ?? '' // <-- requestNumber sebagai requestCode
  isModalOpen.value = true
}
const expanded = ref({})
</script>

<template>
<ModalCancelRequest
  :open="isModalOpen"
  @close="isModalOpen = false"
  @update:open="isModalOpen = $event"
  :status="selectedStatus"
  :requestCode="selectedRequestCode"
    @submitted="handleSubmitted" 

/>
    <UTable
      :data="props.items"
      :columns="columns"
      class="flex-1 border rounded-lg"

      v-model:expanded="expanded"
    >
      <template #expanded="{ row }">
        <div class="bg-gray-900 p-4 rounded-b-lg">
          <div class="flex flex-col gap-2">
            <div>
              <span class="font-semibold text-white">Item Code:</span>
              <span class="ml-2 text-gray-200">{{ row.original.item?.itemCode ?? '-' }}</span>
            </div>
            <div>
              <span class="font-semibold text-white">Item Name:</span>
              <span class="ml-2 text-gray-200">{{ row.original.item?.itemName ?? '-' }}</span>
            </div>
            <div>
              <span class="font-semibold text-white">Quantity:</span>
              <span class="ml-2 text-gray-200">{{ row.original.quantity ?? '-' }}</span>
            </div>
          </div>
        </div>
      </template>
    </UTable>
</template>