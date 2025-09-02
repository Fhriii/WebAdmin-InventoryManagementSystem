<template>
  <div style="display: flex; min-height: 100vh;" orientation="horizontal">
    <div style="width: 220px; padding: 20px 0; position: sticky; top: 0; align-self: flex-start;">
      <Navigation v-if="$route.path !== '/'" />
    </div>
    <div style="flex: 1; padding: 24px;">
          <NuxtPage />
    </div>
</div>
</template>

<script setup>
import Navigation from '~/components/navigation.vue'
import { useRoute } from 'vue-router'
const $route = useRoute()
</script>