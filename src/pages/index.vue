<!-- eslint-disable no-console -->
<script setup>
import axios from 'axios'
import 'vue3-carousel/dist/carousel.css'
import { Carousel, Navigation, Pagination, Slide } from 'vue3-carousel'

defineOptions({
  name: 'IndexPage',
})

const myCarousel = ref(null)

const slides = [
  {
    id: 1,
    src: '/04.jpg',
  },
  {
    id: 2,
    src: '/05.jpg',
  },
  {
    id: 3,
    src: '/06.jpg',
  },
  {
    id: 4,
    src: '/07.jpg',
  },
  {
    id: 5,
    src: '/08.jpg',
  },
  {
    id: 6,
    src: '/09.jpg',
  },
]

const cats = ref([])

onMounted(async () => {
  cats.value = await axios.get('https://avesh.netserve.in/cats').then(r => r.data)
})
</script>

<template>
  <Carousel ref="myCarousel" :items-to-show="1" :autoplay="2000" :wrap-around="true">
    <Slide v-for="slide in slides" :key="slide.id">
      <div class="carousel__item">
        <img :src="slide.src">
      </div>
    </Slide>

    <template #addons>
      <Navigation />
      <Pagination />
    </template>
  </Carousel>

  <div class="mx-auto max-w-7xl px-5 space-y-16 lg-px5 md-px12 sm-px10">
    <div class="max-w-full space-y-3">
      <h1 class="text-3xl/tight text-gray9 font-bold sm-text-4xl/tight dark-text-white">
        Our Products Range
      </h1>
    </div>
    <div class="grid grid-cols-12 gap-4">
      <div v-for="cat in cats" :key="cat.id" class="aspect-5/3.8 relative col-span-12 my-5 w-full overflow-hidden rd-lg md:col-span-4">
        <img :src="`https://avesh.netserve.in/${cat.image_src}`" alt="project cover" class="w-full object-cover">
        <div class="absolute inset-0 flex flex-col justify-end from-gray-800 bg-gradient-to-t p-5 text-gray3 space-y-5 dark:from-gray-900">
          <h1 class="text-2xl text-white font-semibold">
            {{ cat.name }}
          </h1>
          <div class="w-full flex justify-between">
            <a :href="`./cats/${cat.id}`" class="group flex justify-start gap-x-3 border-b border-gray8 text-gray1 font-medium">
              View Products
              <span class="duration-300 ease-linear group-hover:pl-2">
                <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20" fill="currentColor" class="h-5 w-5">
                  <path fill-rule="evenodd" d="M5.22 14.78a.75.75 0 001.06 0l7.22-7.22v5.69a.75.75 0 001.5 0v-7.5a.75.75 0 00-.75-.75h-7.5a.75.75 0 000 1.5h5.69l-7.22 7.22a.75.75 0 000 1.06z" clip-rule="evenodd" />
                </svg>
              </span>
            </a>
            <a :href="`categories/cat-${cat.id}.pdf`" class="group flex justify-end gap-x-3 border-b border-gray8 text-gray1 font-medium">
              View details
              <span class="duration-300 ease-linear group-hover:pl-2">
                <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20" fill="currentColor" class="h-5 w-5">
                  <path fill-rule="evenodd" d="M5.22 14.78a.75.75 0 001.06 0l7.22-7.22v5.69a.75.75 0 001.5 0v-7.5a.75.75 0 00-.75-.75h-7.5a.75.75 0 000 1.5h5.69l-7.22 7.22a.75.75 0 000 1.06z" clip-rule="evenodd" />
                </svg>
              </span>
            </a>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style>
.carousel__item {
  min-height: 200px;
  width: 100%;
  background-color: var(--vc-clr-primary);
  color: var(--vc-clr-white);
  font-size: 20px;
  border-radius: 8px;
  display: flex;
  justify-content: center;
  align-items: center;
}

.carousel__slide {
  padding: 0;
}

.carousel__prev,
.carousel__next {
  box-sizing: content-box;
  border: 0;
}
</style>
