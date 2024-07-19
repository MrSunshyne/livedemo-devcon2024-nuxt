<template>
    <div
      class="shadow-lg flex justify-between space-y-2 border-[1px] border-white/5 bg-sky-950 text-white p-4 rounded-md w-full"
    >
      <!-- {{ props.outage }} -->

      <div class="flex flex-col justify-between gap-2">
        <div class="flex items-center gap-2 w-full">
          <div class="text-xl font-bold">{{ props.outage.locality }}</div>
          <div class="w-6 h-6 relative">
            <div class="absolute inset-0">
              <div class="sr-only">indicator here</div>
            </div>
          </div>
        </div>
        <p class="font-light max-w-xl">
          {{ props.outage.streets }}
        </p>
      </div>
      <div class="flex flex-col justify-between gap-2">
        <!-- <p class="text-right">Power will resume --</p> -->
        <div class="flex flex-col items-end">
          <div class="text-sm">??</div>
          <div class="text-sm font-light text-right">FROM {{ formatDate(props.outage.from) }} TO {{ formatDate(props.outage.to)}}</div>
        </div>
      </div>
    </div>
</template>

<script setup lang="ts">

interface Outage {
  date: string
  locality: string
  streets: string
  district: string
  from: string
  to: string
  id: string
}

interface Props {
  outage: Outage
}
const props = defineProps<Props>()

function formatDate(str: string) {
  let date = new Date(str)
  return date.toLocaleTimeString()
}
</script>