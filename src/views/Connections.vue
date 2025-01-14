<template>
  <div class="space-y-6">
    <header>
      <h1 class="text-3xl font-bold text-gray-900">Connections</h1>
    </header>

    <div class="bg-white shadow rounded-lg">
      <div class="px-4 py-5 sm:px-6 border-b border-gray-200">
        <h2 class="text-lg font-medium text-gray-900">Active Connections</h2>
      </div>
      <ul class="divide-y divide-gray-200">
        <li v-for="connection in connections" :key="connection.id" class="px-4 py-4 sm:px-6">
          <div class="flex items-center justify-between">
            <div class="flex items-center">
              <div class="flex-shrink-0">
                <Building2 class="h-8 w-8 text-gray-400" />
              </div>
              <div class="ml-4">
                <p class="text-sm font-medium text-gray-900">{{ connection.companyName }}</p>
                <p class="text-sm text-gray-500">Connected since {{ connection.connectedSince }}</p>
              </div>
            </div>
            <div class="flex items-center space-x-4">
              <span class="text-sm text-gray-500">
                {{ connection.invoiceCount }} invoices synced
              </span>
              <button class="text-red-600 hover:text-red-700 text-sm font-medium">
                Disconnect
              </button>
            </div>
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>

<script setup lang="ts">
import { Building2 } from 'lucide-vue-next'

const connections = [
  {
    id: 1,
    companyName: 'Acme Corp',
    connectedSince: 'Jan 15, 2024',
    invoiceCount: 45
  },
  {
    id: 2,
    companyName: 'Soylent Corp',
    connectedSince: 'Feb 1, 2024',
    invoiceCount: 23
  }
]
</script>