<script setup lang="ts">
import { StudyEvent } from '@/types'
import { format, startOfDay } from 'date-fns'
import ja from 'date-fns/locale/ja/index.js'

interface Props {
  title: StudyEvent['title']
  catch: StudyEvent['catch']
  event_url: StudyEvent['event_url']
  started_at: StudyEvent['started_at']
  ended_at: StudyEvent['ended_at']
  description: StudyEvent['description']
  limit: StudyEvent['limit']
  accepted: StudyEvent['accepted']
}

const props = defineProps<Props>()

const desc = computed(() => {
  const maxLen = 64
  const div = document.createElement('div')
  div.innerHTML = props.description
  const result = div.innerText.slice(0, maxLen + 1)
  console.log(maxLen)
  return result.length > maxLen ? `${result.slice(0, maxLen)}…` : result
})

const isPast = computed(() => startOfDay(new Date) > new Date(props.ended_at))
const startEnd = computed(() => `${format(new Date(props.started_at), 'HH:mm', { locale: ja })}〜${format(new Date(props.ended_at), 'HH:mm', { locale: ja })}`)

const moveTo = () => {
  window.open(props.event_url, '_blank')
}
</script>

<template>
  <div
    v-if="!isPast"
    class="p-4 md:w-1/2 lg:w-1/3"
  >
    <div
      class="h-full p-4 rounded-xl bg-white shadow hover:(bg-sky-100 shadow-lg cursor-pointer)"
      @click="moveTo"
    >
      <div class="bg-opacity-75 pb-4 overflow-hidden relative">
        <div class="md:flex">
          <client-only>
            <StudyCardItemDate :started_at="props.started_at" />
          </client-only>
          <h1 class="flex-initial title-font sm:text-xl font-medium mb-3">
            {{ props.title }}
          </h1>
        </div>
        <div>
          <p class="font-bold">
            {{ props.catch }}<br>
          </p>
          <p class="leading-relaxed">
            {{ $stripTags(props.description, 256) }}
          </p>
          <p class="text-right">
            <BaseIcon>🧑‍💻</BaseIcon>
            {{ props.accepted != null ? props.accepted : '--' }} / {{ props.limit != null ? props.limit : '--' }}
          </p>
          <p class="text-right">
            <BaseIcon>⏰</BaseIcon>
            <client-only>{{ startEnd }}</client-only>
          </p>
        </div>
      </div>
    </div>
  </div>
</template>
