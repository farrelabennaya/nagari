<script setup lang="ts">
import { ref, onMounted, watch } from "vue";
import { useRoute } from "vue-router";
import { useFlowbite } from '~/composables/useFlowbite';

// initialize components based on data attribute selectors
onMounted(() => {
    useFlowbite(() => {
        initFlowbite();
    })
})

const userDropdownOpen = ref(false);
const nagariDropdownOpen = ref(false);
const pendudukDropdownOpen = ref(false);
const sidebarOpen = ref(false);
const activeMenu = ref("");
const route = useRoute();

const toggleUserDropdown = () => {
  userDropdownOpen.value = !userDropdownOpen.value;
  localStorage.setItem("userDropdownOpen", userDropdownOpen.value);
};

const toggleNagariDropdown = () => {
  nagariDropdownOpen.value = !nagariDropdownOpen.value;
  localStorage.setItem("nagariDropdownOpen", nagariDropdownOpen.value);
};
const togglePendudukDropdown = () => {
  pendudukDropdownOpen.value = !pendudukDropdownOpen.value;
  localStorage.setItem("pendudukDropdownOpen", pendudukDropdownOpen.value);
};

const toggleSidebar = () => {
  sidebarOpen.value = !sidebarOpen.value;
};

const updateActiveMenu = () => {
  activeMenu.value = route.path;
};

onMounted(() => {
  const userDropdownState = localStorage.getItem("userDropdownOpen");
  if (userDropdownState !== null) {
    userDropdownOpen.value = userDropdownState === "true";
  }

  const nagariDropdownState = localStorage.getItem("nagariDropdownOpen");
  if (nagariDropdownState !== null) {
    nagariDropdownOpen.value = nagariDropdownState === "true";
  }
  const pendudukDropdownState = localStorage.getItem("pendudukDropdownOpen");
  if (pendudukDropdownState !== null) {
    pendudukDropdownOpen.value = pendudukDropdownState === "true";
  }
  updateActiveMenu();

// Menghapus status dropdown dari localStorage saat halaman di-refresh
window.addEventListener("beforeunload", () => {
  localStorage.removeItem("userDropdownOpen");
  localStorage.removeItem("nagariDropdownOpen");
  localStorage.removeItem("pendudukDropdownOpen");
});
});

watch(route, () => {
  updateActiveMenu();
});
</script>

<template>
  <!-- Button to toggle sidebar on mobile -->
  <button
    class="fixed top-4 left-4 z-50 sm:hidden"
    @click="toggleSidebar"
    aria-label="Toggle Sidebar"
  >
    <svg
      xmlns="http://www.w3.org/2000/svg"
      class="h-8 w-8 text-gray-500"
      fill="none"
      viewBox="0 0 24 24"
      stroke="currentColor"
      stroke-width="2"
    >
      <path stroke-linecap="round" stroke-linejoin="round" d="M4 6h16M4 12h16m-7 6h7" />
    </svg>
  </button>

  <aside
    id="logo-sidebar"
    :class="[
      'fixed top-0 left-0 z-40 w-64 h-screen pt-20 transition-transform bg-white border-r border-gray-200 dark:bg-gray-800 dark:border-gray-700',
      sidebarOpen ? 'translate-x-0' : '-translate-x-full sm:translate-x-0',
    ]"
    aria-label="Sidebar"
  >
    <div class="h-full px-3 pb-4 overflow-y-auto bg-white dark:bg-gray-800">
      <ul class="space-y-2 font-medium">
        <li>
          <NuxtLink
            to="/admin"
            class="text-base text-gray-900 font-normal rounded-lg flex items-center p-2 hover:bg-gray-100 group"
            :class="{ 'bg-gray-200': activeMenu === '/admin' }"
            @click="sidebarOpen = false"
          >
            <svg
              class="w-6 h-6 text-gray-500 group-hover:text-gray-900 transition duration-75"
              fill="currentColor"
              viewBox="0 0 20 20"
              xmlns="http://www.w3.org/2000/svg"
            >
              <path d="M2 10a8 8 0 018-8v8h8a8 8 0 11-16 0z"></path>
              <path d="M12 2.252A8.014 8.014 0 0117.748 8H12V2.252z"></path>
            </svg>
            <span class="ml-3">Kembali</span>
          </NuxtLink>
        </li>

        <!-- Dropdown User -->
        

        <div class="space-y-2 pt-2"></div>
      </ul>
    </div>
  </aside>
</template>

<style scoped>
/* Styling untuk tampilan mobile dan desktop */
@media (max-width: 640px) {
  #logo-sidebar {
    transform: translateX(-100%);
    transition: transform 0.3s ease-in-out;
  }
  #logo-sidebar.translate-x-0 {
    transform: translateX(0);
  }
}

/* Styling untuk tampilan desktop agar sidebar selalu terlihat */
@media (min-width: 641px) {
  #logo-sidebar {
    transform: translateX(0);
  }
}

.bg-gray-200 {
  background-color: #e5e7eb !important;
}

.custom-bg {
  background-color: #f7b267;
}
</style>
