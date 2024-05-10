<script setup>
const navIsOpen = ref(false)
const navItems = [
  {
    id: 1,
    text: 'Home',
    href: '/',
  },
  {
    id: 2,
    text: 'About Us',
    href: '/about',
  },
  {
    id: 3,
    text: 'Product Range',
    href: '/catagories/1',
  },
  {
    id: 4,
    text: 'Contact',
    href: '/contact',
  },
]

function toggleNavBar() {
  navIsOpen.value = !navIsOpen.value
}
function closeNavBar() {
  navIsOpen.value = false
}
</script>

<template>
  <div aria-hidden="true" bg="gray-8/40" class="fixed inset-0 z30" :class="navIsOpen ? 'visible flex lg-hidden lg-invisible' : 'invisible hidden'" @click="closeNavBar()" />
  <header
    border-b="~ gray-1 dark:gray-9" bg="blue-200/80 dark:gray-950/80"
    class="sticky top-0 z40 h20 w-full flex items-center backdrop-blur-xl backdrop-filter"
  >
    <nav px="5 sm:10 md:12 lg:5" class="relative mxauto max-w-7xl w-full flex items-center justify-between gap-x-5">
      <div class="min-w-max flex items-center">
        <a href="/" class="relative flex items-center gap-2.5">
          <span class="flex">
            <img h12 w12 src="/avesh-logo.png">
          </span>
          <span text="indigo-950 dark:white" inline-flex text-lg font-bold>
            Avesh
          </span>
        </a>
      </div>
      <div
        lg="top-0 relative w-max flex" bg="white dark:gray-950 lg:transparent"
        border-b="~ gray-2 dark:gray-8 lg:none" py="8 lg:0" px="5 sm:10 md:12 lg:px-0"
        class="absolute left-0 top-full w-full gap-x-6 duration-300 ease-linear lg-transition-none"
        :class="navIsOpen ? 'visible op100 translate-y-0' : 'translate-y-10 lg-translate-y-0 invisible lg-visible op0 lg-op100'"
      >
        <ul text="gray-7 dark:gray-3" class="flex flex-col gap6 lg-w-full lg-flex-row lg-items-center lg-justify-center">
          <li v-for="navItem in navItems" :key="navItem.id">
            <router-link :to="navItem.href" class="after-ease-linean relative py2.5 duration-300 ease-linear after-absolute after-bottom-0 after-left-0 after-h-px after-w-full after-rd-md after-bg-indigo-6 hover-text-indigo-6 after-duration-300 after-content-empty" :class="navItem.isActive ? 'text-indigo-6 after-scale-x-100' : 'after-scale-x-0 hover-after-scale-x-100'">
              {{ navItem.text }}
            </router-link>
          </li>
        </ul>
      </div>
      <div flex items-center lg-hidden>
        <button
          border-l="~ indigo-1 dark:gray-7" relative
          bg-transparent p-3 outline-none aria-label="toggle navbar" @click="toggleNavBar()"
        >
          <div h0.5 w6 rd bg="gray-7 dark:gray-3" transition duration-300 aria-hidden="true" :class="navIsOpen ? 'rotate-45 translate-y-1.5' : ''" />
          <div mt2 h0.5 w6 rd bg="gray-7 dark:gray-3" transition duration-300 aria-hidden="true" :class="navIsOpen ? '-rotate-45 -translate-y-1.5' : ''" />
        </button>
      </div>
    </nav>
  </header>
</template>
