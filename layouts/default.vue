<template>
  <div class="min-h-screen p-4 sm:p-8 bg-nuxt2-dark">
    <div class="container mx-auto min-h-full box-border p-4 sm:p-8 rounded-lg bg-gray-100 text-gray-700">
      <TheHeader/>
      <Nuxt />
      <slot />
      <TheFooter v-if="$route.path !== '/'" />
    </div>
  </div>
</template>
