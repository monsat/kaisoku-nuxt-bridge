<script setup lang="ts">
interface Props {
  to?: string
}

const props = withDefaults(defineProps<Props>(), {
  to: '/'
})
</script>

<template>
  <NuxtLink
    :to="props.to"
    class="text-nuxt-dark active:text-nuxt-dark hover:(opacity-75 underline)"
  >
    <slot>快速 Nuxt Bridge の TOPページ</slot>
  </NuxtLink>
</template>
