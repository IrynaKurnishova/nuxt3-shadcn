<template>
  <div>
    <div class="flex z-50 items-center justify-between w-full h-full p-4 lg:hidden">
      <Logo/>
      <Icon
          @click="open = true"
          class="z-50 cursor-pointer left-2 top-2"
          size="30"
          name="iconamoon:menu-burger-horizontal"
      />
      <div
          v-if="open"
          class="fixed top-0 left-0 z-[999] bg-white w-full h-full h-screen"
      >
        <Icon
            @click="open = false"
            class="absolute z-50 cursor-pointer right-4 top-4"
            size="30"
            name="material-symbols:close"
        />
        <SidebarMenu/>
      </div>
    </div>
    <div class="hidden lg:flex w-[250px] h-screen flex flex-col justify-between border-r">
      <SidebarMenu/>
      <div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
const open = ref(true)
</script>
