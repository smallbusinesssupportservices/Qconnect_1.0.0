<template>
  <div class="space-y-6">
    <header>
      <h1 class="text-3xl font-bold text-gray-900">Settings</h1>
    </header>

    <div class="bg-white shadow rounded-lg divide-y divide-gray-200">
      <!-- QuickBooks Integration -->
      <div class="p-6">
        <h2 class="text-lg font-medium text-gray-900 mb-4">QuickBooks Integration</h2>
        <div class="flex items-center justify-between">
          <div>
            <p class="text-sm text-gray-500">Connected to QuickBooks Online</p>
            <p class="text-xs text-gray-400">Last synced: March 15, 2024 at 2:30 PM</p>
          </div>
          <button class="px-4 py-2 text-sm font-medium text-blue-600 bg-blue-50 rounded-md hover:bg-blue-100">
            Reconnect
          </button>
        </div>
      </div>

      <!-- Notification Settings -->
      <div class="p-6">
        <h2 class="text-lg font-medium text-gray-900 mb-4">Notifications</h2>
        <div class="space-y-4">
          <div class="flex items-center justify-between">
            <div>
              <p class="text-sm font-medium text-gray-700">Email Notifications</p>
              <p class="text-sm text-gray-500">Receive notifications about new invoices</p>
            </div>
            <button 
              class="relative inline-flex h-6 w-11 flex-shrink-0 cursor-pointer rounded-full border-2 border-transparent transition-colors duration-200 ease-in-out focus:outline-none focus:ring-2 focus:ring-blue-500 focus:ring-offset-2"
              :class="[emailNotifications ? 'bg-blue-600' : 'bg-gray-200']"
              @click="emailNotifications = !emailNotifications"
            >
              <span 
                class="pointer-events-none inline-block h-5 w-5 transform rounded-full bg-white shadow ring-0 transition duration-200 ease-in-out"
                :class="[emailNotifications ? 'translate-x-5' : 'translate-x-0']"
              />
            </button>
          </div>
        </div>
      </div>

      <!-- Company Information -->
      <div class="p-6">
        <h2 class="text-lg font-medium text-gray-900 mb-4">Company Information</h2>
        <form class="space-y-4">
          <div>
            <label for="company-name" class="block text-sm font-medium text-gray-700">Company Name</label>
            <input
              type="text"
              id="company-name"
              v-model="companyInfo.name"
              class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-blue-500 focus:ring-blue-500 sm:text-sm"
            />
          </div>
          <div>
            <label for="company-email" class="block text-sm font-medium text-gray-700">Business Email</label>
            <input
              type="email"
              id="company-email"
              v-model="companyInfo.email"
              class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-blue-500 focus:ring-blue-500 sm:text-sm"
            />
          </div>
          <div class="flex justify-end">
            <button type="submit" class="px-4 py-2 text-sm font-medium text-white bg-blue-600 rounded-md hover:bg-blue-700">
              Save Changes
            </button>
          </div>
        </form>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const emailNotifications = ref(true)
const companyInfo = ref({
  name: 'Your Company Name',
  email: 'contact@yourcompany.com'
})
</script>