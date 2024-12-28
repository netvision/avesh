<!-- eslint-disable no-alert -->
<script setup>
import axios from 'axios'
import Datepicker from 'vue3-datepicker'

const data = ref('')
const cats = ref([])
const feed = ref({})
feed.value.date = ref(new Date())
feed.value.cur_date = ref(new Date())
const submitted = ref(false)

const resetFeed = () => feed.value = {}

async function saveFeed() {
  if (!feed.value.name) {
    alert ('Name cannot be empty')
  }
  else if (!feed.value.mobile) {
    alert('Phone cannot be empty')
  }
  else if (!feed.value.problem) {
    alert ('Please write some feedback in message field')
  }

  else if (!feed.value.model_no) {
    alert ('Please mention product model no')
  }

  else if (!feed.value.product_name) {
    alert ('Please mention product name')
  }

  else {
    feed.value.date_of_purchase = feed.value.date.toISOString().slice(0, 10)
    feed.value.cur_date = feed.value.cur_date.toISOString().slice(0, 10)
    const res = await axios.post('https://avesh.netserve.in/complaints', feed.value)
    submitted.value = true
    if (res.status === 201)
      alert('form submitted!')
  }
}

onMounted(async () => {
  data.value = await axios.get('https://avesh.netserve.in/website-infos/1').then(r => r.data)
  cats.value = await axios.get('https://avesh.netserve.in/cats').then(r => r.data)
})
</script>

<template>
  <div class="mx-auto max-w-3xl px-5 space-y-16 lg-px5 md-px12 sm-px10">
    <h2 mx-5 border-b-2 p-2 text-left text-3xl font-bold>
      Raise a <span class="text-red-700 italic">Complaint</span>
    </h2>
    <div v-if="!submitted" class="grid grid-cols-1 m-6 gap-4 gap-y-2 text-left text-sm text-xl md:grid-cols-5">
      <div class="md:col-span-5">
        <label for="subject">Date</label>
        <Datepicker v-model="feed.cur_date" class="mt-1 h-10 w-full border rounded bg-gray-50 px-4" />
      </div>
      <div class="md:col-span-5">
        <label for="name">Customer / Dealer Name</label>
        <input v-model="feed.name" type="text" name="name" class="mt-1 h-10 w-full border rounded bg-gray-50 px-4" value="" placeholder="Name">
      </div>

      <div class="md:col-span-5">
        <label for="mobile">Mobile No.</label>
        <input v-model="feed.mobile" type="text" name="mobile" class="mt-1 h-10 w-full border rounded bg-gray-50 px-4" value="" placeholder="Mobile">
      </div>

      <div class="md:col-span-5">
        <label for="alt_mobile">Alternate Mobile No</label>
        <input v-model="feed.alt_mobile" type="text" name="alt_mobile" class="mt-1 h-10 w-full border rounded bg-gray-50 px-4" value="" placeholder="Alt Mobile">
      </div>

      <div class="md:col-span-5">
        <label for="address">Address</label>
        <input v-model="feed.address" type="text" name="address" class="mt-1 h-10 w-full border rounded bg-gray-50 px-4" value="" placeholder="Address">
      </div>

      <div class="md:col-span-5">
        <label for="district">District</label>
        <input v-model="feed.district" type="text" name="district" class="mt-1 h-10 w-full border rounded bg-gray-50 px-4" value="" placeholder="District">
      </div>

      <div class="md:col-span-5">
        <label for="state">State</label>
        <input v-model="feed.state" type="text" name="state" class="mt-1 h-10 w-full border rounded bg-gray-50 px-4" placeholder="State">
      </div>

      <div class="md:col-span-5">
        <label for="pin">Pincode</label>
        <input v-model="feed.pin" type="text" name="pin" class="mt-1 h-10 w-full border rounded bg-gray-50 px-4" placeholder="Pincode">
      </div>

      <div class="md:col-span-5">
        <label for="pin">Product Category</label>
        <select v-model="feed.product_name" placeholder="Select product category" class="block border border-gray-400 rounded-md bg-white p-2 text-gray-700 transition-colors duration-200 focus:border-blue-600 hover:border-gray-500 focus:ring-2 focus:ring-blue-600">
          <option v-for="cat in cats" :key="cat.id" :value="cat.name">
            {{ cat.name }}
          </option>
        </select>
      </div>

      <div class="md:col-span-5">
        <label for="Model No.">Model No.</label>
        <input v-model="feed.model_no" type="text" name="product" class="mt-1 h-10 w-full border rounded bg-red-50 px-4" placeholder="Model No.">
      </div>

      <div class="md:col-span-5">
        <label for="serial_no">Serial No.</label>
        <input v-model="feed.serial_no" type="text" name="serial" class="mt-1 h-10 w-full border rounded bg-red-50 px-4" placeholder="Serial">
      </div>

      <div class="md:col-span-5">
        <label for="subject">Date Of Purchase</label>
        <Datepicker v-model="feed.date" class="mt-1 h-10 w-full border rounded bg-gray-50 px-4" />
      </div>
      <div class="md:col-span-5">
        <label for="problem">Complaint in Product</label>
        <textarea id="problem" v-model="feed.problem" rows="4" class="block w-full border border-gray-300 rounded-lg bg-gray-50 p-2.5 text-sm text-gray-900 dark:border-gray-600 focus:border-blue-500 dark:bg-gray-700 dark:text-white focus:ring-blue-500 dark:focus:border-blue-500 dark:focus:ring-blue-500 dark:placeholder-gray-400" placeholder="describe the problem in product here..." />
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
      <p>Thank you <span class="font-bold">{{ feed.name }}</span> for sharing your concern. We will getback to you soon and resolve your issue at the earliest!</p>
      <p>
        <router-link to="/">
          Click to get back to home Page
        </router-link>
      </p>
    </div>
  </div>
</template>
