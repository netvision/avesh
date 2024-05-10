<script setup>
import axios from 'axios'

const data = ref('')

onMounted(async () => {
  data.value = await axios.get('https://avesh.netserve.in/website-infos/1').then(r => r.data)
})
</script>

<template>
  <h2 mx-5 border-b-2 p-2 text-left text-3xl font-bold>
    Contact Info
  </h2>
  <div mx-5 p-5 text-left text-lg line-height-relaxed>
    <p text-xl font-bold>
      {{ data.title }}
    </p>
    <p italic>
      {{ data.slogan }}
    </p>
    <p>{{ data.full_address }}</p>
    <p>Phone: {{ data.phone1 }}</p>
    <p>WhatsApp No.: {{ data.whatsapp }}</p>
    <p>Email: {{ data.email_id }}</p>
  </div>
</template>
