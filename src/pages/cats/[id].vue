<script setup>
import axios from 'axios'
import 'vue3-carousel/dist/carousel.css'
import { Carousel, Navigation, Slide } from 'vue3-carousel'

const data = ref([])
const params = useRoute('/catagories/[id]').params
const selectedTab = ref(+params.id)

function selectTab(id) {
  selectedTab.value = id
}

onMounted(async () => {
  data.value = await axios.get('https://avesh.netserve.in/cats?expand=products').then((r) => {
    const data = r.data.map((item) => {
      if (item.products.length > 0) {
        item.products = item.products.map((prod) => {
          return {
            ...prod,
            imgs: JSON.parse(prod.img_urls),
          }
        })
        return item
      }
      else { return item }
    })
    return data
  },
  )
})
</script>

<template>
  <div class="mt-5 flex">
    <!-- Tabs -->
    <div class="ml-5 min-w-32 w-1/5 flex flex-col border-r">
      <div
        v-for="tab in data"
        :key="tab.id"
        class="cursor-pointer p-4 text-left" :class="[{ 'bg-blue-500 text-white': tab.id === selectedTab, 'hover:bg-gray-200': tab.id !== selectedTab }]"
        @click="selectTab(tab.id)"
      >
        {{ tab.name }}
      </div>
    </div>
    <!-- Tab Content -->
    <div class="flex-1 p-4">
      <div v-for="tab in data" v-show="tab.id === selectedTab" :key="tab.id">
        <section>
          <div class="mx-auto max-w-full px-5 space-y-16 lg-px5 md-px12 sm-px10">
            <div v-if="tab?.name" class="text-left space-y-3">
              <h1 class="text-3xl/tight text-gray9 font-bold sm-text-4xl/tight dark-text-white">
                {{ tab?.name }}
              </h1>
              <p class="text-gray7 dark-text-gray3">
                {{ tab?.description }}
              </p>
            </div>
            <div v-if="tab.products && tab.products?.length > 0" class="grid gap6 lg-grid-cols-4 md-grid-cols-3 sm-grid-cols-2 lg-gap10 md-gap8">
              <div v-for="prod in tab.products" :key="prod.id" class="relative border border-gray2 rd-lg bg-gray1 p-5 space-y-6 dark-border-gray8 dark-bg-gray9 md:p-8 sm:p-6">
                <Carousel v-if="prod.imgs.length > 1" :items-to-show="1" :autoplay="2000" :wrap-around="true">
                  <Slide v-for="(im, i) in prod.imgs" :key="i">
                    <div class="carousel__item">
                      <img :src="im.url">
                    </div>
                  </Slide>

                  <template #addons>
                    <Navigation />
                  </template>
                </Carousel>
                <img v-else :src="prod.imgs[0].url" alt="project cover" width="1300" class="aspect-[4/3.3] w-full rounded object-cover">
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
  </div>
</template>
