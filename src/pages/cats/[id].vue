<!-- eslint-disable antfu/top-level-function -->
<!-- eslint-disable no-console -->
<script setup>
import axios from 'axios'
import 'vue3-carousel/dist/carousel.css'
import { Carousel, Navigation, Slide } from 'vue3-carousel'

const params = useRoute('/catagories/[id]').params

const data = ref({})
const curCat = ref({})
const products = ref([])

const getCatData = async (id) => {
  products.value = []
  curCat.value = await data.value.find(d => d.id === id)

  products.value = await axios.get(`https://avesh.netserve.in/prods?filter[cat_id][eq]=${id}`).then((r) => {
    return r.data.map((d) => {
      return { ...d, img: JSON.parse(d.img_urls) }
    })
  })

  console.log(products.value)
}

onMounted(async () => {
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
            <h1 v-if="curCat" class="text-3xl/tight text-gray9 font-bold sm-text-4xl/tight dark-text-white">
              {{ curCat.name }}
            </h1>
            <p v-if="curCat" class="text-gray7 dark-text-gray3">
              {{ curCat?.description }}
            </p>
          </div>
          <div v-if="products && products?.length > 0" class="grid gap6 lg-grid-cols-4 md-grid-cols-3 sm-grid-cols-2 lg-gap10 md-gap8">
            <div v-for="prod in products" :key="prod.id" class="relative border border-gray2 rd-lg bg-gray1 p-5 space-y-6 dark-border-gray8 dark-bg-gray9 md:p-8 sm:p-6">
              <Carousel v-if="prod.img.length > 1" :items-to-show="1" :autoplay="2000" :wrap-around="true">
                <Slide v-for="(im, i) in prod.img" :key="i">
                  <div class="carousel__item">
                    <img :src="im.url">
                  </div>
                </Slide>

                <template #addons>
                  <Navigation />
                </template>
              </Carousel>
              <img v-else :src="prod.img[0].url" alt="project cover" width="1300" class="aspect-[4/3.3] w-full rounded object-cover">
              <div class="space-y5 flex flex-col justify-end text-gray3">
                <h1 class="text-lg text-gray9 font-semibold dark-text-white">
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
