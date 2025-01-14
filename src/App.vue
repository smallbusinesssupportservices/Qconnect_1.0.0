<template>
  <div class="min-h-screen bg-gray-50">
    <nav class="bg-white shadow-sm">
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div class="flex justify-between h-16">
          <div class="flex items-center">
            <Link class="w-8 h-8 text-blue-600" />
            <span class="ml-2 text-xl font-semibold text-gray-900">QuickBooks Connect</span>
          </div>
          <div class="flex items-center space-x-4">
            <router-link 
              v-for="item in navigation" 
              :key="item.name"
              :to="item.href"
              class="px-3 py-2 rounded-md text-sm font-medium hover:bg-gray-100"
              :class="[
                $route.path === item.href
                  ? 'text-blue-600 bg-blue-50'
                  : 'text-gray-700'
              ]"
            >
              {{ item.name }}
            </router-link>
          </div>
        </div>
      </div>
    </nav>

    <main class="max-w-7xl mx-auto py-6 sm:px-6 lg:px-8">
      <router-view></router-view>
    </main>
  </div>
</template>

<script setup lang="ts">
import { Link } from 'lucide-vue-next'

const navigation = [
  { name: 'Dashboard', href: '/' },
  { name: 'Vendors', href: '/vendors' },
  { name: 'Connections', href: '/connections' },
  { name: 'Settings', href: '/settings' }
]
</script>