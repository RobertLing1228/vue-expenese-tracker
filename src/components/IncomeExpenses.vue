<template>
  <div class="inc-exp-container">
    <div class="">
      <h4>Income</h4>
      <p id="money-plus" class="money plus">+${{ totalIncome }}</p>
    </div>
    <div>
      <h4>Expense</h4>
      <p id="money-minus" class="money minus">-${{ totalExpense }}</p>
    </div>
  </div>
</template>

<script setup lang="ts">
import { defineProps } from "vue";
const props = defineProps({
  totalIncome: {
    type: Number,
    required: true,
  },
  totalExpense: {
    type: Number,
    required: true,
  },
});
</script>

<style scoped></style>
