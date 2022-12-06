<script setup lang="ts">
defineProps<{
  label: Float32List;
}>();
</script>

<template>
  <div class="flex flex-col mb-6">
    <label class="font-medium mb-3">{{ label }}</label>
    <slot />
  </div>
</template>

