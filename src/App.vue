<script setup>
import { computed, ref } from 'vue'
import CountdownHeader from '@/components/CountdownHeader.vue'
import CountdownSegment from './components/CountdownSegment.vue'
import { useNow } from '@vueuse/core'

const now = ref(useNow())
const christmas = ref(new Date('12/25/2022 00:00:00'))

const isChristmas = computed(() => {
  return christmas.value.getDate() - 1 - now.value.getDate() < 0
})

const timeDiff = computed(() => {
  if (isChristmas.value) {
    return {
      days: 0,
      hours: 0,
      minutes: 0,
      seconds: 0,
    }
  }
  return {
    days: christmas.value.getDate() - 1 - now.value.getDate(),
    hours: 23 - now.value.getHours(),
    minutes: 59 - now.value.getMinutes(),
    seconds: 59 - now.value.getSeconds(),
  }
})
</script>
<template>
  <div class="w-full h-full flex justify-center items-center p-10">
    <div>
      <div class="shadow-md relative bg-white p-5 rounded-lg border-gray-100 border-[1px]">
        <CountdownHeader />
        <main v-if="!isChristmas" class="flex justify-center">
          <CountdownSegment label="days" :number="timeDiff.days" />
          <CountdownSegment label="hours" :number="timeDiff.hours" />
          <CountdownSegment label="minutes" :number="timeDiff.minutes" />
          <CountdownSegment label="seconds" :number="timeDiff.seconds" />
        </main>
        <main v-else class="flex justify-center">
          <h2>Merry Christmas!</h2>
        </main>
      </div>
      <h4 class="mt-10 text-gray-400 text-center text-sm">
        This challenge brought to you by <a href="https://vueschool.io/" class="underline">Vue School</a>
      </h4>
    </div>
  </div>
</template>

<style>
div {
  display: block;
}

body {
  @apply bg-gray-100;
}
</style>
