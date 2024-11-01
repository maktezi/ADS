<template>
  <div>
    <NuxtPage />
  </div>
</template>

<script setup lang="ts">
import {definePageMeta} from "#imports";

const isMobile = ref(false);
const checkIfMobile = () => {
  isMobile.value = window.innerWidth <= 768
}
onMounted (() => {
  checkIfMobile();
  window.addEventListener('resize', checkIfMobile);
})
provide('isMobile', isMobile)

useHead({
  title: 'Compare Our Top 3 VPNs'
})
</script>