<template>
  <the-header />
  <main p-0 font-sans text="center gray-700 dark:gray-200">
    <RouterView :key="$route.fullPath" />
  </main>
  <TheFooter />
</template>
