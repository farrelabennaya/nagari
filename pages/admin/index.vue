<template>
  <div>
    <AppHeader />
    <div class="flex overflow-hidden bg-white pt-16">
      <SidebarAdmin />
      <div
        id="main-content"
        class="h-full w-full bg-gray-50 relative overflow-y-auto sm:ml-64"
      >
      <div class="custom-header to-gray-100 p-6 pb-32 pt-5">
        <main>
          <div class="pt-6 px-4">
            <h1 class="text-2xl font-bold mb-6">Dashboard</h1>
            <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6">
              <div
                class="bg-white rounded-lg shadow-lg p-6 hover:shadow-xl transition-shadow cursor-pointer"
                @click="navigateTo('/admin/users')"
              >
                <div class="flex items-center">
                  <div class="bg-blue-500 text-white p-3 rounded-full">
                    <i class="fas fa-users"></i>
                  </div>
                  <div class="ml-4">
                    <h5 class="text-lg font-semibold">Users</h5>
                    <p class="text-gray-500">Manage Users</p>
                  </div>
                </div>
              </div>

              <div
                class="bg-white rounded-lg shadow-lg p-6 hover:shadow-xl transition-shadow cursor-pointer"
                @click="navigateTo('/admin/reports')"
              >
                <div class="flex items-center">
                  <div class="bg-red-500 text-white p-3 rounded-full">
                    <i class="fas fa-chart-line"></i>
                  </div>
                  <div class="ml-4">
                    <h5 class="text-lg font-semibold">Reports</h5>
                    <p class="text-gray-500">View Reports</p>
                  </div>
                </div>
              </div>

              <div
                class="bg-white rounded-lg shadow-lg p-6 hover:shadow-xl transition-shadow cursor-pointer"
                @click="navigateTo('/admin/settings')"
              >
                <div class="flex items-center">
                  <div class="bg-green-500 text-white p-3 rounded-full">
                    <i class="fas fa-cogs"></i>
                  </div>
                  <div class="ml-4">
                    <h5 class="text-lg font-semibold">Settings</h5>
                    <p class="text-gray-500">System Settings</p>
                  </div>
                </div>
              </div>

              <div
                class="bg-white rounded-lg shadow-lg p-6 hover:shadow-xl transition-shadow cursor-pointer"
                @click="navigateTo('/admin/help')"
              >
                <div class="flex items-center">
                  <div class="bg-yellow-500 text-white p-3 rounded-full">
                    <i class="fas fa-question-circle"></i>
                  </div>
                  <div class="ml-4">
                    <h5 class="text-lg font-semibold">Help</h5>
                    <p class="text-gray-500">Get Assistance</p>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </main>
        </div>

        
      </div>
    </div>
  </div>
</template>

<script setup>
import { useRouter } from 'vue-router';
import AppHeader from '~/components/AppHeader.vue';
import SidebarAdmin from '~/components/SidebarAdmin.vue';
definePageMeta({
  middleware: ["auth", "role"],
  colorMode: "light",
});

const router = useRouter();

const navigateTo = (path) => {
  router.push(path);
};
</script>

<style scoped>
.custom-bg-main {
  background-color: #f9fafb;
}

.custom-header {
  background: linear-gradient(to right, #adc4ce, #e0ebf0);
}
</style>