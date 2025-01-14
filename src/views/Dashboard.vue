<template>
  <div class="space-y-6">
    <header>
      <h1 class="text-3xl font-bold text-gray-900">Dashboard</h1>
    </header>

    <div class="grid grid-cols-1 gap-6 sm:grid-cols-2 lg:grid-cols-3">
      <!-- Stats Cards -->
      <router-link 
        v-for="stat in stats" 
        :key="stat.name" 
        :to="stat.link"
        class="bg-white overflow-hidden shadow rounded-lg hover:bg-gray-50 transition-colors duration-200"
      >
        <div class="p-5">
          <div class="flex items-center">
            <div class="flex-shrink-0">
              <component :is="stat.icon" class="h-6 w-6 text-gray-400" />
            </div>
            <div class="ml-5 w-0 flex-1">
              <dl>
                <dt class="text-sm font-medium text-gray-500 truncate">{{ stat.name }}</dt>
                <dd class="text-lg font-semibold text-gray-900">{{ stat.value }}</dd>
              </dl>
            </div>
          </div>
        </div>
      </router-link>
    </div>

    <!-- Unconnected Vendors -->
    <div class="bg-white shadow rounded-lg">
      <div class="px-4 py-5 sm:px-6 flex justify-between items-center">
        <h2 class="text-lg font-medium text-gray-900">Unconnected Vendors</h2>
        <button class="px-4 py-2 text-sm font-medium text-white bg-blue-600 rounded-md hover:bg-blue-700">
          Sync Vendors
        </button>
      </div>
      <ul class="divide-y divide-gray-200">
        <li v-for="vendor in unconnectedVendors" :key="vendor.id" class="px-4 py-4 sm:px-6">
          <div class="flex items-center justify-between">
            <div>
              <p class="text-sm font-medium text-gray-900">{{ vendor.name }}</p>
              <p class="text-sm text-gray-500">{{ vendor.email }}</p>
            </div>
            <button class="px-4 py-2 text-sm font-medium text-blue-600 bg-blue-50 rounded-md hover:bg-blue-100">
              Connect
            </button>
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>

<script setup lang="ts">
import { Users, Receipt, Link } from 'lucide-vue-next'

const stats = [
  { name: 'Connected Vendors', value: '12', icon: Users, link: '/vendors?filter=connected' },
  { name: 'Pending Invites', value: '4', icon: Link, link: '/vendors?filter=pending' },
  { name: 'Recent Invoices', value: '28', icon: Receipt, link: '/connections' }
]

const unconnectedVendors = [
  { id: 1, name: 'Acme Corp', email: 'billing@acmecorp.com' },
  { id: 2, name: 'Globex Corporation', email: 'accounts@globex.com' },
  { id: 3, name: 'Soylent Corp', email: 'finance@soylent.com' }
]
</script>