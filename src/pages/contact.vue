<!-- eslint-disable no-console -->
<!-- eslint-disable no-alert -->
<script setup>
import axios from 'axios'

const data = ref('')
const feed = ref({})
const submitted = ref(false)

const resetFeed = () => feed.value = {}

async function saveFeed() {
  if (!feed.value.full_name) {
    alert ('Name cannot be empty')
  }
  else if (!feed.value.phone) {
    alert('Phone cannot be empty')
  }
  else if (!feed.value.feed) {
    alert ('Please write some feedback in message field')
  }
  else {
    feed.value.date = new Date().toISOString().slice(0, 10)
    const res = await axios.post('https://avesh.netserve.in/feedbacks', feed.value)
    submitted.value = true
    if (res.status === 201)
      await axios.post('https://avesh.netserve.in/feedback/mail')
  }
}

onMounted(async () => {
  data.value = await axios.get('https://avesh.netserve.in/website-infos/1').then(r => r.data)
})
</script>

<template>
  <div class="mx-auto max-w-7xl flex items-start px-5 space-y-16 lg-px5 md-px12 sm-px10">
    <div class="w-1/2">
      <h2 mx-5 p-2 text-left text-3xl font-bold>
        Send us a <span class="text-blue-800 italic">Feedback</span>
      </h2>
      <div v-if="!submitted" class="grid grid-cols-1 m-6 gap-4 gap-y-2 text-left text-sm text-xl md:grid-cols-5">
        <div class="md:col-span-5">
          <label for="full_name">Full Name</label>
          <input v-model="feed.full_name" type="text" name="full_name" class="mt-1 h-10 w-full border rounded bg-gray-50 px-4" value="">
        </div>

        <div class="md:col-span-5">
          <label for="firm">Firm/Business Info</label>
          <input v-model="feed.firm" type="text" name="firm" class="mt-1 h-10 w-full border rounded bg-gray-50 px-4" value="" placeholder="name of the Firm or Business">
        </div>

        <div class="md:col-span-5">
          <label for="email">Email Address</label>
          <input v-model="feed.email" type="text" name="email" class="mt-1 h-10 w-full border rounded bg-gray-50 px-4" value="" placeholder="email@domain.com">
        </div>

        <div class="md:col-span-5">
          <label for="phone">Phone</label>
          <input v-model="feed.phone" type="text" name="phone" class="mt-1 h-10 w-full border rounded bg-gray-50 px-4" value="" placeholder="Phone no.">
        </div>

        <div class="md:col-span-5">
          <label for="address">Full Address</label>
          <input v-model="feed.location" type="text" name="address" class="mt-1 h-10 w-full border rounded bg-gray-50 px-4" value="" placeholder="Full Address">
        </div>

        <div class="md:col-span-5">
          <label for="subject">Topic</label>
          <input v-model="feed.subject" type="text" name="subject" class="mt-1 h-10 w-full border rounded bg-gray-50 px-4" value="" placeholder="Topic/subject">
        </div>
        <div class="md:col-span-5">
          <label for="message">Your message</label>
          <textarea id="message" v-model="feed.feed" rows="4" class="block w-full border border-gray-300 rounded-lg bg-gray-50 p-2.5 text-sm text-gray-900 dark:border-gray-600 focus:border-blue-500 dark:bg-gray-700 dark:text-white focus:ring-blue-500 dark:focus:border-blue-500 dark:focus:ring-blue-500 dark:placeholder-gray-400" placeholder="Your message..." />
        </div>
        <div class="text-right md:col-span-5">
          <div class="inline-flex items-end">
            <button class="mr-4 rounded bg-blue-500 px-4 py-2 text-white font-bold hover:bg-blue-700" @click="resetFeed">
              Reset
            </button>
            <button class="rounded bg-blue-500 px-4 py-2 text-white font-bold hover:bg-blue-700" @click="saveFeed">
              Submit
            </button>
          </div>
        </div>
      </div>
      <div v-else>
        <p>Thank you {{ feed.full_name }} for the feedback. we will getback to you soon!</p>
        <p>
          <router-link to="/">
            Click to get back to home Page
          </router-link>
        </p>
      </div>
    </div>
    <div>
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
    </div>
  </div>
</template>
