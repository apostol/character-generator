<script setup lang="ts">
import { ref } from 'vue'

defineProps<{
  prompt: string
  message: string
  height: number
  weight: number
  position: {
    x: number
    y: number
  }
}>()
const msg = ref('')
</script>

<template>
  <textarea class="friends" placeholder="{{ prompt }}">{{ message }}</textarea>
</template>

<style scoped>
.read-the-docs {
  color: #888;
}
</style>
