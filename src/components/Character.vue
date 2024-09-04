<script setup lang="ts">
import Write from './Write.vue'
const props = defineProps<{
  image: string
}>()
</script>

<template>
  <img class="page" :src=image>
    <Write />
  </img>
</template>
