<template>
  <nav mt-6 w-full inline-flex justify-center gap-2 text-xl>
    <button icon-btn @click="toggleDark()">
      <div i-carbon-sun dark:i-carbon-moon />
    </button>
  </nav>
</template>
