<script setup lang="ts">
import { usePrefetched } from '@/composables/usePrefetched'
import { useStudyEvent } from '@/composables/useStudyEvent'

const router = useRouter()

usePrefetched()

const {
  events,
  fetched,
  fetchEvents,
} = useStudyEvent()

onMounted(async () => {
  const onError = () => router.push('/')
  await fetchEvents(onError)
})
</script>

<template>
  <div>
    <div v-if="events.length > 0">
      <div>
        <TheH1 icon="📆">
          勉強会カレンダー
        </TheH1>
        <p>
          <BaseLink href="https://connpass.com/">connpass API</BaseLink>
          の勉強会情報をサーバーを通して取得しています。
        </p>
        <p>
          API 取得日時 :
          <client-only>{{ fetched }}</client-only>
        </p>
        <BaseInfo class="my-8">
          <template #head>
            後日修正
          </template>
          <ul class="list-disc list-inside">
            <li>一部 Hydrate に失敗する</li>
          </ul>
        </BaseInfo>
      </div>
      <LineDivide/>
      <StudyCard :events="events" />
    </div>
  </div>
</template>
