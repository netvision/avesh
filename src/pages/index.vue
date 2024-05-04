<script setup>
import 'vue3-carousel/dist/carousel.css'
import { Carousel, Navigation, Pagination, Slide } from 'vue3-carousel'

defineOptions({
  name: 'IndexPage',
})
const slides = [
  {
    id: 1,
    src: '/01.jpg',
  },
  {
    id: 2,
    src: '/02.jpg',
  },
  {
    id: 3,
    src: '/03.jpg',
  },
]
</script>

<template>
  <Carousel :items-to-show="1" :autoplay="2000">
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
  <section class="py24">
    <div class="mx-auto max-w-7xl flex flex-col gap16 px-5 md-flex-row lg-px-5 md-px-12 sm-px-10">
      <div class="flex md-flex-1">
        <p>Image</p>
      </div>
      <div class="text-gray-7 lg-w-54% md-w-1/2 space-y-12 dark-text-gray-3">
        <h1 class="text-2xl text-gray9 font-semibold md-text-4xl sm-text-3xl dark-text-white">
          We help drive your business forward faster
        </h1>
        <p>
          Lorem ipsum, dolor sit amet consectetur adipisicing elit. Minus, saepe aliquid autem alias vero
          distinctio dignissimos consequatur? Excepturi quibusdam, quam ipsum hic, laudantium ducimus suscipit,
          culpa facere consequuntur repellat delectus.
        </p>
        <div class="grid gap6 sm-grid-cols-2">
          <div class="border border-gray1 rd-xl bg-white p4 space-y-6 dark-border-gray9 dark-bg-gray-950">
            <span class="w-max flex rd-full bg-gray-9 p3 text-gray1 dark-bg-gray1 dark-text-gray9">
              <svg
                xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5"
                stroke="currentColor" class="h6 w6"
              >
                <path
                  stroke-linecap="round" stroke-linejoin="round"
                  d="M9.813 15.904L9 18.75l-.813-2.846a4.5 4.5 0 00-3.09-3.09L2.25 12l2.846-.813a4.5 4.5 0 003.09-3.09L9 5.25l.813 2.846a4.5 4.5 0 003.09 3.09L15.75 12l-2.846.813a4.5 4.5 0 00-3.09 3.09zM18.259 8.715L18 9.75l-.259-1.035a3.375 3.375 0 00-2.455-2.456L14.25 6l1.036-.259a3.375 3.375 0 002.455-2.456L18 2.25l.259 1.035a3.375 3.375 0 002.456 2.456L21.75 6l-1.035.259a3.375 3.375 0 00-2.456 2.456zM16.894 20.567L16.5 21.75l-.394-1.183a2.25 2.25 0 00-1.423-1.423L13.5 18.75l1.183-.394a2.25 2.25 0 001.423-1.423l.394-1.183.394 1.183a2.25 2.25 0 001.423 1.423l1.183.394-1.183.394a2.25 2.25 0 00-1.423 1.423z"
                />
              </svg>
            </span>
            <h2 class="text-xl text-gray9 font-semibold dark-text-white">
              Our mission
            </h2>
            <p>
              Lorem ipsum dolor sit amet consectetur
            </p>
          </div>

          <div class="border border-gray1 rd-xl bg-white p-4 space-y-6 dark-border-gray9 dark-bg-gray-950">
            <span class="wmax flex rd-full bg-gray9 p3 text-gray-1 dark-bg-gray1 dark-text-gray9">
              <svg
                xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5"
                stroke="currentColor" class="h6 w6"
              >
                <path
                  stroke-linecap="round" stroke-linejoin="round"
                  d="M2.036 12.322a1.012 1.012 0 010-.639C3.423 7.51 7.36 4.5 12 4.5c4.638 0 8.573 3.007 9.963 7.178.07.207.07.431 0 .639C20.577 16.49 16.64 19.5 12 19.5c-4.638 0-8.573-3.007-9.963-7.178z"
                />
                <path stroke-linecap="round" stroke-linejoin="round" d="M15 12a3 3 0 11-6 0 3 3 0 016 0z" />
              </svg>
            </span>
            <h2 class="text-xl text-gray-9 font-semibold dark-text-white">
              Our vision
            </h2>
            <p>
              Lorem ipsum dolor sit amet consectetur
            </p>
          </div>
        </div>
      </div>
    </div>
  </section>
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
  padding: 10px;
}

.carousel__prev,
.carousel__next {
  box-sizing: content-box;
  border: 5px solid white;
}
</style>
