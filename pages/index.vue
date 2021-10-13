<script setup>

const counter = ref(0)

const inc = () => counter.value++

const hello = ref('')

onBeforeMount(async () => {
  hello.value = await $fetch('/api/hello')
})
</script>

<template>
  <div>
    <div class="p-4">
      <h1>Hello, Bridge !</h1>
      <h2>{{ counter }}</h2>
      <button
        class="py-1 px-4 rounded shadow hover:shadow-none border border-red-200 bg-red-100"
        @click="inc"
      >Inc</button>
      <h3>{{ hello }}</h3>
    </div>
    <Tutorial/>
  </div>
</template>
