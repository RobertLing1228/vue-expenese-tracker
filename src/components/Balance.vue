<template>
  <div class="container">
    <h4>Your Balance</h4>
    <h1 id="balance">{{ balance.toFixed(2) }}</h1>
  </div>
</template>

<script setup lang="ts">
const props = defineProps({
  balance: {
    type: Number,
    required: true,
  },
});
</script>

<style scoped></style>
