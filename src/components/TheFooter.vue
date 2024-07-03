<script setup>
import axios from 'axios'

const info = ref({})
const cats = ref([])
const contact = ref({})

onMounted(async () => {
  const data = await axios.get('https://avesh.netserve.in/website-infos/1').then(r => r.data)
  contact.value = data
  if (data)
    info.value = JSON.parse(data.social_media)
  cats.value = await axios.get('https://avesh.netserve.in/cats').then(r => r.data)
})
</script>

<template>
  <footer bg="gray-1 dark:gray-9" un-text="gray-7 dark:gray-3">
    <div px="5 sm:10 md:12 lg:5" class="grid grid-cols-2 mx-auto max-w-7xl gap-12 py20 lg-grid-cols-6 lg-gap-16">
      <div class="col-span-2 space-y-6">
        <a href="#">
          <img src="/whatsapp-qr.png" class="max-w-xs w-auto">
        </a>
      </div>
      <div class="col-span-2 space-y-2">
        <p pt-10 text-xl font-bold>
          {{ contact.title }}
        </p>
        <p italic>
          {{ contact.slogan }}
        </p>
        <p>{{ contact.full_address }}</p>
        <p>Phone: {{ contact.phone1 }}</p>
        <p>WhatsApp No.: {{ contact.whatsapp }}</p>
        <p>Email: {{ contact.email_id }}</p>
        <h1 un-text="lg gray-9 dark:gray-1" class="pt-5 font-semibold">
          News-letter
        </h1>
        <form class="max-w-2xl w-full flex flex-col gap-3 sm-flex-row">
          <input type="email" placeholder="johndoe@gmail.com" bg="gray-2 dark:gray-8" class="flex-1 rd-md px5 py2.5 outline-none">
          <button class="w-full flex items-center justify-center rd-md bg-blue-6 px5 py2.5 text-white outline-none sm-w-max">
            Subscribe
          </button>
        </form>
      </div>
      <div class="col-span-2 pl-10 space-y-6">
        <h1 un-text="lg gray-9 dark:gray-1" class="pt-10 font-semibold">
          Products Categories
        </h1>
        <ul class="space-y-3">
          <li v-for="item in cats" :key="item.id" class="border-b border-gray-500 hover:bg-gray-200">
            <router-link :to="`/cats/${item.id}`" un-text="hover:blue-6 dark:hover:blue-5" class="duration-200">
              {{ item.name }}
            </router-link>
          </li>
        </ul>
      </div>
    </div>
    <div px="5 sm:10 md:12 lg:5" class="mx-auto max-w-7xl">
      <div border-t="~ gray-2 dark:gray-8" text="gray-7 dark:gray-3" class="w-full flex flex-col items-center gap-4 py3 md-flex-row sm:justify-between">
        <div text="center sm:left" class="flex sm-min-w-max">
          <p> &copy; 2024 Avesh. All right reserved </p>
        </div>
        <div class="w-full flex justify-center gap-3 sm-justify-end">
          <a href="https://avesh.netserve.in/app-release.apk" target="_blank" aria-label="social link">
            <span flex text-2xl>Android App</span>
          </a>
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
