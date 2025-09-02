<script setup lang="ts">
import type { NavigationMenuItem } from '@nuxt/ui'

const items = ref<NavigationMenuItem[][]>([
  [
 
    {
      label: 'Home',
      icon: 'i-lucide-book-open',
      children: [
      
        {
          label: 'Dashboard',
          description: 'Learn how to install and configure Nuxt UI in your application.',
          icon: 'i-lucide-cloud-download',
          to: '/dashboard'
        },
        {
          label: 'Icons',
          icon: 'i-lucide-smile',
          description: 'You have nothing to do, @nuxt/icon will handle it automatically.'
        }
      ]
    },
    {
      label: 'Inventory',
      icon: 'i-lucide-database',
      children: [
        {
          label: 'Item',
          icon: 'i-lucide-file-text',
          description: 'Define shortcuts for your application.',
          to: '/itemmaster'
        },
        {
          label: 'Inventory In',
          icon: 'i-lucide-file-text',
          description: 'Display a modal/slideover within your application.',
          to: '/inventory-in'
        },
        {
          label: 'Inventory Out',
          icon: 'i-lucide-file-text',
          description: 'Display a toast within your application.',
          to: '/inventory-out'
        }
      ]
    },
    {
      label: 'Purchase Order',
      icon: 'i-lucide-box',
      to: '/purchase'

    },
    {
      label: 'Production',
      icon: 'i-lucide-factory',
      to: '/production'
    },
     {
      label: 'Delivery',
      icon: 'i-lucide-truck',
      to: '/delivery'
    },
     {
      label: 'Request Order',
      icon: 'i-lucide-dollar-sign',
      to: '/requestorder'
    },
  ],
  [
    {
      label: 'GitHub',
      icon: 'i-simple-icons-github',
      badge: '3.8k',
      to: 'https://github.com/nuxt/ui',
      target: '_blank'
    },
    {
      label: 'Help',
      icon: 'i-lucide-circle-help',
      disabled: true
    }
  ]
])
</script>

<template>
  <UNavigationMenu  orientation="vertical" :items="items" class="ml-4" />
</template>
