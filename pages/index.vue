<script setup lang="ts">
import { onBeforeMount, ref } from '#app'
import H2 from '~~/components/The/H2.vue'

const counter = ref(0)

const inc = () => counter.value++

const hello = ref('')

onBeforeMount(async () => {
  hello.value = await $fetch('/api/hello')
})
</script>

<template>
  <div>
    <TheH1>Nuxt Bridge パブリック beta リリース 🎉</TheH1>
    <p>
      2021年10月12日（火）の23:00（日本時間）に、待望の
      <BaseLink href="https://v3.nuxtjs.org/">Nuxt 3 ベータ</BaseLink>
      と一緒に
      <BaseLink href="https://v3.nuxtjs.org/getting-started/bridge/">Nuxt Bridge</BaseLink>
      もリリースされました。
    </p>
    <p>
      このサイトは、いち早く Nuxt Bridge を理解したい方のために Nuxt Bridge を使用して構築したサイトです。
    </p>
    <p>
      Nuxt Bridge を使ってどんなことができるか知りたい方は、ぜひゆっくりしていってくださいね☕
    </p>
    <BaseInfo class="my-8">
      <template #head>当サイトのソースコードは GitHub で確認いただけます</template>
      <p>
        Nuxt Bridge は、日々いくつもの修正が行われています。
        このサイトのリポジトリより
        <BaseCode>npm install</BaseCode>
        しても Nuxt Bridge の細かいバージョンの違いにより別の動作をする可能性があることをご確認くださいませ。
      </p>
      <p>
        <BaseLink href="https://github.com/monsat/kaisoku-nuxt-bridge" />
      </p>
      <p>
        バグを見つけたという方、よりよいコードを知っているという方は、ぜひともお知らせくださいませ。
      </p>
    </BaseInfo>
    <div class="my-8">
      <TheH2 icon="🧮">Composition API によるカウンター</TheH2>
      <h2>{{ counter }}</h2>
      <button
        class="py-1 px-4 rounded shadow border border-nuxt-default bg-nuxt-lighter hover:(shadow-none bg-nuxt-default text-nuxt-100 font-bold)"
        @click="inc"
      >Inc</button>
    </div>
    <div class="my-8">
      <TheH2 icon="⚙️">$fetch: /api/hello</TheH2>
      <div>{{ hello }}</div>
    </div>
  </div>
</template>
