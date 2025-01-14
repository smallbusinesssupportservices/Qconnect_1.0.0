<template>
  <div class="space-y-6">
    <header class="flex justify-between items-center">
      <div>
        <h1 class="text-3xl font-bold text-gray-900">Vendors</h1>
        <p class="mt-1 text-sm text-gray-500">
          {{ filterDescription }}
        </p>
      </div>
      <button class="px-4 py-2 text-sm font-medium text-white bg-blue-600 rounded-md hover:bg-blue-700">
        Add Vendor
      </button>
    </header>

    <div class="bg-white shadow rounded-lg">
      <div class="px-4 py-5 sm:px-6 border-b border-gray-200">
        <div class="flex items-center justify-between">
          <h2 class="text-lg font-medium text-gray-900">{{ listTitle }}</h2>
          <div class="flex space-x-2">
            <button 
              v-for="filter in filters" 
              :key="filter.value"
              @click="currentFilter = filter.value"
              :class="[
                'px-3 py-1 text-sm font-medium rounded-md',
                currentFilter === filter.value
                  ? 'bg-blue-100 text-blue-700'
                  : 'text-gray-500 hover:text-gray-700'
              ]"
            >
              {{ filter.label }}
            </button>
          </div>
        </div>
      </div>
      <ul class="divide-y divide-gray-200">
        <li v-for="vendor in filteredVendors" :key="vendor.id" class="px-4 py-4 sm:px-6">
          <div class="flex items-center justify-between">
            <div>
              <p class="text-sm font-medium text-gray-900">{{ vendor.name }}</p>
              <p class="text-sm text-gray-500">{{ vendor.email }}</p>
              <p class="text-xs text-gray-400">Last invoice: {{ vendor.lastInvoice }}</p>
            </div>
            <div class="flex items-center space-x-4">
              <span :class="[
                'px-2 py-1 text-xs font-medium rounded-full',
                vendor.status === 'Connected' ? 'bg-green-100 text-green-800' : 'bg-gray-100 text-gray-800'
              ]">
                {{ vendor.status }}
              </span>
              <button class="text-gray-400 hover:text-gray-500">
                <Settings class="h-5 w-5" />
              </button>
            </div>
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, computed, onMounted } from 'vue'
import { Settings } from 'lucide-vue-next'
import { useRoute } from 'vue-router'

const route = useRoute()
const currentFilter = ref(route.query.filter as string || 'all')

const filters = [
  { label: 'All', value: 'all' },
  { label: 'Connected', value: 'connected' },
  { label: 'Pending', value: 'pending' }
]

const vendors = [
  { 
    id: 1, 
    name: 'Acme Corp', 
    email: 'billing@acmecorp.com',
    status: 'Connected',
    lastInvoice: 'March 15, 2024'
  },
  { 
    id: 2, 
    name: 'Globex Corporation', 
    email: 'accounts@globex.com',
    status: 'Pending',
    lastInvoice: 'March 10, 2024'
  },
  { 
    id: 3, 
    name: 'Soylent Corp', 
    email: 'finance@soylent.com',
    status: 'Connected',
    lastInvoice: 'March 8, 2024'
  },
  { 
    id: 4, 
    name: 'Initech', 
    email: 'accounts@initech.com',
    status: 'Connected',
    lastInvoice: 'March 5, 2024'
  }
]

const filteredVendors = computed(() => {
  if (currentFilter.value === 'all') return vendors
  return vendors.filter(vendor => 
    vendor.status.toLowerCase() === currentFilter.value
  )
})

const listTitle = computed(() => {
  switch (currentFilter.value) {
    case 'connected':
      return 'Connected Vendors'
    case 'pending':
      return 'Pending Vendors'
    default:
      return 'All Vendors'
  }
})

const filterDescription = computed(() => {
  switch (currentFilter.value) {
    case 'connected':
      return 'Showing all vendors with active connections'
    case 'pending':
      return 'Showing vendors with pending invitations'
    default:
      return 'Showing all vendors'
  }
})

onMounted(() => {
  if (route.query.filter) {
    currentFilter.value = route.query.filter as string
  }
})
</script>