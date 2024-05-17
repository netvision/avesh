<!-- eslint-disable antfu/top-level-function -->
<!-- eslint-disable no-console -->
<script setup>
import axios from 'axios'

const params = useRoute('/catagories/[id]').params

const data = ref({})
const curCat = ref({})
const getCatData = async (id) => {
  curCat.value = {}
  curCat.value = await axios.get(`https://avesh.netserve.in/cats/${id}?expand=products`).then(r => r.data)
  console.log(curCat.value)
}

onMounted(async () => {
  console.log(params.id)
  data.value = await axios.get(`https://avesh.netserve.in/cats`).then(r => r.data)
  await getCatData(params.id)
})
</script>

<template>
  <div flex justify-between>
    <div w="20%" bg-blue-100>
      <h2 class="pt-6 text-2xl/tight text-gray9 font-bold sm-text-2xl/tight dark-text-white">
        Product Categories
      </h2>
      <div v-for="cat in data" :key="cat.id" cursor-pointer p-5 hover-bg-white @click="getCatData(cat.id)">
        <img :src="`https://avesh.netserve.in/${cat.image_src}`" w-48 object-cover>
        <h3 text-left text-xl font-bold>
          {{ cat.name }}
        </h3>
      </div>
    </div>
    <div w="80%">
      <section class="py-20">
        <div class="mx-auto max-w-full px-5 space-y-16 lg-px5 md-px12 sm-px10">
          <div class="text-left space-y-3">
            <h1 class="text-3xl/tight text-gray9 font-bold sm-text-4xl/tight dark-text-white">
              {{ curCat.name }}
            </h1>
            <p class="text-gray7 dark-text-gray3">
              {{ curCat.description }}
            </p>
          </div>
          <div v-if="curCat.products && curCat.products?.length > 0" class="grid gap6 lg-grid-cols-3 sm-grid-cols-2 lg-gap10 md-gap8">
            <div v-for="prod in curCat.products" :key="prod.id" class="relative border border-gray2 rd-lg bg-gray1 p-5 space-y-6 dark-border-gray8 dark-bg-gray9 md:p-8 sm:p-6">
              <img :src="JSON.parse(prod.img_urls)[0].url" alt="project cover" width="1300" class="aspect-[4/3.3] w-full rounded object-cover">
              <div class="space-y5 flex flex-col justify-end text-gray3">
                <h1 class="text-2xl text-gray9 font-semibold dark-text-white">
                  {{ prod.name }}
                </h1>
                <p class="line-clamp-2 text-gray7 dark-text-gray3">
                  {{ prod.description }}
                </p>
              </div>
            </div>
          </div>
        </div>
      </section>
    </div>
  </div>
</template>
