<template>
<div>
  <header class="items-center flex gap-2 p-4 hover:scale-[101%] transition cursor-pointer">
    <Logo/>
    <p class="font-bold text-black">Nuxt Project</p>
  </header>
  <div class="px-4 grow">
    <div class="grid gap-2">
      <NuxtLink
          :href="item.path"
          v-for="(item, index) in items"
          :key="index"
          class="flex items-center gap-2 px-2 py-1 transition rounded cursor-pointer hover:bg-neutral-100"
      >
        <Icon size="20" :name="item.icon" color="black"/>
        <span>{{item.title}}</span>
      </NuxtLink>
    </div>
  </div>
</div>
</template>

<script setup lang="ts">
const items= ref([
  {
    title: "Overview",
    path: "/",
    icon: "ri:dashboard-line"
  },
  {
    title: "Transactions",
    path: "/transactions",
    icon: "clarity:two-way-arrows-line"
  },
  {
    title: "Account",
    path: "/account",
    icon: "solar:settings-minimalistic-linear"
  },
  {
    title: "Contacts",
    path: "/contacts",
    icon: "mdi:account-box-outline"
  },
  {
    title: "Settings",
    path: "/settings",
    icon: "ic:outline-settings"
  },

])
</script>

