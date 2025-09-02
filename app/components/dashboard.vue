<!-- pages/admin/index.vue -->
<template>
  <div class="min-h-screen ">
   
    <div >
      <!-- Header -->
      <header class=" shadow-sm border-b border-gray-200">
        <div class="flex items-center justify-between px-6 py-4">
          <h2 class="text-2xl font-semibold text-white">Dashboard</h2>
          <div class="flex items-center space-x-4">
            <button class="p-2 text-gray-400 hover:text-white">
              <svg class="w-6 h-6" fill="currentColor" viewBox="0 0 20 20">
                <path d="M10 2a6 6 0 00-6 6v3.586l-.707.707A1 1 0 004 14h12a1 1 0 00.707-1.707L16 11.586V8a6 6 0 00-6-6zM10 18a3 3 0 01-3-3h6a3 3 0 01-3 3z"/>
              </svg>
            </button>
            <div class="flex items-center space-x-2">
              <div class="w-8 h-8 bg-blue-500 rounded-full flex items-center justify-center">
                <span class="text-white text-sm font-medium">JD</span>
              </div>
              <span class="text-sm font-medium text-gray-700">John Doe</span>
            </div>
          </div>
        </div>
      </header>

      <!-- Dashboard Content -->
      <main class="p-6">
        <!-- Stats Cards -->
        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6 mb-8">
          <div class=" rounded-lg shadow p-6">
            <div class="flex items-center justify-between">
              <div>
                <p class="text-sm font-medium text-white">Total Users</p>
                <p class="text-3xl font-bold text-white">{{ stats.totalUsers.toLocaleString() }}</p>
              </div>
              <div class="w-12 h-12 bg-blue-100 rounded-lg flex items-center justify-center">
                <svg class="w-6 h-6 text-blue-600" fill="currentColor" viewBox="0 0 20 20">
                  <path fill-rule="evenodd" d="M10 9a3 3 0 100-6 3 3 0 000 6zm-7 9a7 7 0 1114 0H3z" clip-rule="evenodd"/>
                </svg>
              </div>
            </div>
            <div class="mt-4">
              <span class="text-green-600 text-sm font-medium">+12%</span>
              <span class="text-white text-sm">from last month</span>
            </div>
          </div>

          <div class=" rounded-lg shadow p-6">
            <div class="flex items-center justify-between">
              <div>
                <p class="text-sm font-medium text-white">Revenue</p>
                <p class="text-3xl font-bold text-white">${{ stats.revenue.toLocaleString() }}</p>
              </div>
              <div class="w-12 h-12 bg-green-100 rounded-lg flex items-center justify-center">
                <svg class="w-6 h-6 text-green-600" fill="currentColor" viewBox="0 0 20 20">
                  <path fill-rule="evenodd" d="M4 4a2 2 0 00-2 2v4a2 2 0 002 2V6h10a2 2 0 00-2-2H4zm2 6a2 2 0 012-2h8a2 2 0 012 2v4a2 2 0 01-2 2H8a2 2 0 01-2-2v-4zm6 4a2 2 0 100-4 2 2 0 000 4z" clip-rule="evenodd"/>
                </svg>
              </div>
            </div>
            <div class="mt-4">
              <span class="text-green-600 text-sm font-medium">+8.2%</span>
              <span class="text-white text-sm">from last month</span>
            </div>
          </div>

          <div class=" rounded-lg shadow p-6">
            <div class="flex items-center justify-between">
              <div>
                <p class="text-sm font-medium text-white">Orders</p>
                <p class="text-3xl font-bold text-white">{{ stats.orders.toLocaleString() }}</p>
              </div>
              <div class="w-12 h-12 bg-yellow-100 rounded-lg flex items-center justify-center">
                <svg class="w-6 h-6 text-yellow-600" fill="currentColor" viewBox="0 0 20 20">
                  <path fill-rule="evenodd" d="M6 2a1 1 0 00-1 1v1H4a2 2 0 00-2 2v10a2 2 0 002 2h12a2 2 0 002-2V6a2 2 0 00-2-2h-1V3a1 1 0 10-2 0v1H7V3a1 1 0 00-1-1zm0 5a1 1 0 000 2h8a1 1 0 100-2H6z" clip-rule="evenodd"/>
                </svg>
              </div>
            </div>
            <div class="mt-4">
              <span class="text-red-600 text-sm font-medium">-3.1%</span>
              <span class="text-white text-sm">from last month</span>
            </div>
          </div>

          <div class=" rounded-lg shadow p-6">
            <div class="flex items-center justify-between">
              <div>
                <p class="text-sm font-medium text-white">Conversion Rate</p>
                <p class="text-3xl font-bold text-white">{{ stats.conversionRate }}%</p>
              </div>
              <div class="w-12 h-12 bg-purple-100 rounded-lg flex items-center justify-center">
                <svg class="w-6 h-6 text-purple-600" fill="currentColor" viewBox="0 0 20 20">
                  <path fill-rule="evenodd" d="M3 3a1 1 0 000 2v8a2 2 0 002 2h2.586l-1.293 1.293a1 1 0 101.414 1.414L10 15.414l2.293 2.293a1 1 0 001.414-1.414L12.414 15H15a2 2 0 002-2V5a1 1 0 100-2H3zm11.707 4.707a1 1 0 00-1.414-1.414L10 9.586 8.707 8.293a1 1 0 00-1.414 1.414l2 2a1 1 0 001.414 0l4-4z" clip-rule="evenodd"/>
                </svg>
              </div>
            </div>
            <div class="mt-4">
              <span class="text-green-600 text-sm font-medium">+2.4%</span>
              <span class="text-white text-sm">from last month</span>
            </div>
          </div>
        </div>

        <!-- Charts and Tables Row -->
        <div class="grid grid-cols-1 lg:grid-cols-2 gap-8 mb-8">
          <!-- Chart -->
          <div class=" rounded-lg shadow p-6">
            <h3 class="text-lg font-semibold text-white mb-4">Revenue Trend</h3>
            <div class="h-64 flex items-end justify-between space-x-2">
              <div v-for="(value, index) in chartData" :key="index" class="bg-blue-500 rounded-t flex-1 transition-all duration-300 hover:bg-blue-600" :style="{ height: `${(value / Math.max(...chartData)) * 100}%` }"></div>
            </div>
            <div class="flex justify-between mt-2 text-sm text-white">
              <span>Jan</span>
              <span>Feb</span>
              <span>Mar</span>
              <span>Apr</span>
              <span>May</span>
              <span>Jun</span>
            </div>
          </div>

          <!-- Recent Activity -->
          <div class=" rounded-lg shadow p-6">
            <h3 class="text-lg font-semibold text-white mb-4">Recent Activity</h3>
            <div class="space-y-4">
              <div v-for="activity in recentActivities" :key="activity.id" class="flex items-center space-x-3">
                <div class="w-8 h-8 bg-gray-200 rounded-full flex items-center justify-center">
                  <svg class="w-4 h-4 text-white" fill="currentColor" viewBox="0 0 20 20">
                    <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm3.707-9.293a1 1 0 00-1.414-1.414L9 10.586 7.707 9.293a1 1 0 00-1.414 1.414l2 2a1 1 0 001.414 0l4-4z" clip-rule="evenodd"/>
                  </svg>
                </div>
                <div class="flex-1">
                  <p class="text-sm font-medium text-white">{{ activity.action }}</p>
                  <p class="text-xs text-gray-500">{{ activity.time }}</p>
                </div>
              </div>
            </div>
          </div>
        </div>

        <!-- Recent Orders Table -->
        <div class=" rounded-lg shadow">
          <div class="px-6 py-4 border-b border-gray-200">
            <h3 class="text-lg font-semibold text-white">Recent Orders</h3>
          </div>
          <div class="overflow-x-auto">
            <table class="w-full">
              <thead class="">
                <tr>
                  <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Order ID</th>
                  <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Customer</th>
                  <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Product</th>
                  <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Amount</th>
                  <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Status</th>
                  <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Date</th>
                </tr>
              </thead>
              <tbody class=" divide-y divide-gray-200">
                <tr v-for="order in recentOrders" :key="order.id" class="hover:bg-gray-500">
                  <td class="px-6 py-4 whitespace-nowrap text-sm font-medium text-white">#{{ order.id }}</td>
                  <td class="px-6 py-4 whitespace-nowrap text-sm text-white">{{ order.customer }}</td>
                  <td class="px-6 py-4 whitespace-nowrap text-sm text-white">{{ order.product }}</td>
                  <td class="px-6 py-4 whitespace-nowrap text-sm text-white">${{ order.amount }}</td>
                  <td class="px-6 py-4 whitespace-nowrap">
                    <span :class="getStatusClass(order.status)" class="px-2 inline-flex text-xs leading-5 font-semibold rounded-full">
                      {{ order.status }}
                    </span>
                  </td>
                  <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">{{ order.date }}</td>
                </tr>
              </tbody>
            </table>
          </div>
        </div>
      </main>
    </div>
  </div>
</template>

<script setup>
// Page meta for Nuxt 4
definePageMeta({
  layout: false
})

// Reactive data
const stats = reactive({
  totalUsers: 12450,
  revenue: 84720,
  orders: 1847,
  conversionRate: 3.24
})

const chartData = reactive([45, 67, 89, 34, 78, 56])

const recentActivities = reactive([
  { id: 1, action: 'New user registered', time: '2 minutes ago' },
  { id: 2, action: 'Order #1847 completed', time: '15 minutes ago' },
  { id: 3, action: 'Product inventory updated', time: '1 hour ago' },
  { id: 4, action: 'Payment received', time: '2 hours ago' },
  { id: 5, action: 'New review posted', time: '3 hours ago' }
])

const recentOrders = reactive([
  { id: '1847', customer: 'John Smith', product: 'Laptop Pro', amount: '1,299', status: 'Completed', date: '2024-08-28' },
  { id: '1846', customer: 'Sarah Johnson', product: 'Wireless Headphones', amount: '199', status: 'Processing', date: '2024-08-28' },
  { id: '1845', customer: 'Mike Wilson', product: 'Smart Watch', amount: '399', status: 'Shipped', date: '2024-08-27' },
  { id: '1844', customer: 'Emma Davis', product: 'Tablet', amount: '649', status: 'Completed', date: '2024-08-27' },
  { id: '1843', customer: 'David Brown', product: 'Gaming Mouse', amount: '79', status: 'Cancelled', date: '2024-08-26' }
])

// Helper function for status styling
const getStatusClass = (status) => {
  switch (status.toLowerCase()) {
    case 'completed':
      return 'bg-green-100 text-green-800'
    case 'processing':
      return 'bg-yellow-100 text-yellow-800'
    case 'shipped':
      return 'bg-blue-100 text-blue-800'
    case 'cancelled':
      return 'bg-red-100 text-red-800'
    default:
      return 'bg-gray-100 text-white'
  }
}

// SEO Head
useHead({
  title: 'Admin Dashboard',
  meta: [
    { name: 'description', content: 'Admin dashboard for managing your application' }
  ]
})
</script>

<style scoped>
/* Custom scrollbar for better UX */
::-webkit-scrollbar {
  width: 6px;
  height: 6px;
}

::-webkit-scrollbar-track {
  background: #f1f1f1;
}

::-webkit-scrollbar-thumb {
  background: #c1c1c1;
  border-radius: 3px;
}

::-webkit-scrollbar-thumb:hover {
  background: #a1a1a1;
}
</style>