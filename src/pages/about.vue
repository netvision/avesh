<script setup>
import axios from 'axios'

const about = ref('')

onMounted(async () => {
  about.value = await axios.get('https://avesh.netserve.in/website-infos/1').then(r => r.data)
})
</script>

<template>
  <div class="mx-auto max-w-7xl px-5 space-y-16 lg-px5 md-px12 sm-px10">
    <h2 mx-5 border-b-2 p-2 text-left text-3xl font-bold>
      About Us
    </h2>
    <div mx-5 p-2 text-justify text-lg v-html="about.about_us" />
  </div>
</template>
