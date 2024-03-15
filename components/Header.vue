<script setup lang="ts">
const nuxtApp = useNuxtApp()
const {updateHeadings } = useScrollspy()

nuxtApp.hooks.hookOnce('page:finish', () => {
  updateHeadings([
    document.querySelector('#features'),
    document.querySelector('#pricing'),
    document.querySelector('#testimonials'),
    document.querySelector('#faq')
  ])
})
</script>

<template>
  <UHeader>
    <template #logo>
      TabooGenerate <UBadge label="Community" variant="subtle" class="mb-0.5" />
    </template>
  </UHeader>
</template>
