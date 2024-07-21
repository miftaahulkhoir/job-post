<script setup>
import { computed, ref, watch } from "vue";
import { RouterLink, useRoute } from "vue-router";

import logo from "@/assets/img/logo.png";

const route = useRoute();

const initialMenus = ref([
  {
    name: "Home",
    path: "/",
    isActive: true,
  },
  {
    name: "Jobs",
    path: "/jobs",
    isActive: false,
  },
  {
    name: "Add Job",
    path: "/jobs/add",
    isActive: false,
  }
])


const menus = computed(() => {
  return initialMenus.value.map(menu => ({
    ...menu,
    isActive: menu.path === route.path
  }));
});
</script>

<template>
  <nav class="bg-green-700 border-b border-green-500">
    <div class="mx-auto max-w-7xl px-2 sm:px-6 lg:px-8">
      <div class="flex h-20 items-center justify-between">
        <div class="flex flex-1 items-center justify-center md:items-stretch">
          <RouterLink class="flex flex-shrink-0 items-center mr-4" to="/">
            <img class="h-10 w-auto" :src="logo" alt="Vue Jobs">
            <span class="hidden md:block text-white text-2xl font-bold ml-2">Vue Jobs</span>
          </RouterLink>
          <div class="md:ml-auto">
            <div class="flex space-x-2">
              <RouterLink v-for="menu in menus" :to="menu.path"
                :class="[menu.isActive ? 'bg-green-900' : 'hover:bg-gray-900 hover:text-white', 'text-white', 'px-3', 'py-2', 'rounded-md']">
                {{ menu.name }}
              </RouterLink>
            </div>
          </div>
        </div>
      </div>
    </div>
  </nav>
</template>