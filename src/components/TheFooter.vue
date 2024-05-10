<script setup>
import axios from 'axios'

const info = ref({})

onMounted(async () => {
  const data = await axios.get('https://avesh.netserve.in/website-infos/1').then(r => r.data)
  if (data)
    info.value = JSON.parse(data.social_media)
})
</script>

<template>
  <footer bg="gray-1 dark:gray-9" un-text="gray-7 dark:gray-3" bottom-0 m-5 w-full>
    <div px="5 sm:10 md:12 lg:5" class="mx-auto max-w-7xl">
      <div border-t="~ gray-2 dark:gray-8" text="gray-7 dark:gray-3" class="w-full flex flex-col items-center gap-4 py3 md-flex-row sm:justify-between">
        <div text="center sm:left" class="flex sm-min-w-max">
          <p> &copy; 2024 AVESH. All right reserved </p>
        </div>
        <div class="w-full flex justify-center gap-3 sm-justify-end">
          <a v-if="info.twitter" :href="info.twitter" aria-label="social link">
            <span i-carbon-logo-twitter flex text-2xl />
          </a>
          <a v-if="info.linkedin" :href="info.linkedin" aria-label="social link">
            <span i-carbon-logo-linkedin flex text-2xl />
          </a>
          <a v-if="info.instagram" :href="info.instagram" aria-label="social link">
            <span i-carbon-logo-instagram flex text-2xl />
          </a>
          <a :href="info.facebook" aria-label="social link">
            <span i-carbon-logo-facebook flex text-2xl />
          </a>
          <button icon-btn @click="toggleDark()">
            <div i-carbon-sun dark:i-carbon-moon />
          </button>
        </div>
      </div>
    </div>
  </footer>
</template>
