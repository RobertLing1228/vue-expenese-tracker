<template>
  <h3>History</h3>
  <ul id="list" class="list">
    <li
      v-for="transaction in transactions"
      :key="transaction.id"
      :class="transaction.amount < 0 ? 'minus' : 'plus'"
    >
      {{ transaction.text }} <span>$ {{ transaction.amount }}</span>
      <button class="delete-btn" @click="deleteTransaction(transaction.id)">
        x
      </button>
    </li>
  </ul>
</template>

<script setup lang="ts">
import type { Transaction } from "../types";
import { defineProps, ref, defineEmits } from "vue";

const emit = defineEmits(["deleteTransactionSuccess"]);

const props = defineProps({
  transactions: {
    type: Array as () => Transaction[],
    required: true,
  },
});
let transactions = ref(props.transactions);

const deleteTransaction = (id: number) => {
  transactions.value = transactions.value.filter(
    (transaction) => transaction.id !== id
  );
  emit("deleteTransactionSuccess", id);
};
</script>

<style scoped></style>
