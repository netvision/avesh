<script setup>
import axios from 'axios'

const params = useRoute('/catagories/[id]').params

const data = ref({})

onMounted(async () => {
  data.value = await axios.get(`https://avesh.netserve.in/cats/${params.id}?expand=products`).then(r => r.data)
})
</script>

<template>
  <div flex justify-between>
    <div w="25%">
      <div p-5>
        <img :src="`https://avesh.netserve.in/${data.image_src}`" w-full object-cover>
        <h3 text-xl font-bold>
          {{ data.name }}
        </h3>
      </div>
    </div>
    <div w="75%">
      <div v-if="data.products?.length > 0" p-5>
        <pre>{{ data.products }}</pre>
      </div>
      <div v-else p-5>
        <p>Coming soon...</p>
      </div>
    </div>
  </div>
</template>
