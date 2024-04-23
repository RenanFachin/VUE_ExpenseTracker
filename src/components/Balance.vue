<script setup>
const props = defineProps({
  total: {
    type: Number,
    required: true,
  }
})
</script>

<template>
  <h4 class="text-zinc-600 font-bold text-sm">Your Balance</h4>
  <h1 id="balance" class="text-zinc-900 font-bold text-3xl">$ {{ total }}</h1>
</template>