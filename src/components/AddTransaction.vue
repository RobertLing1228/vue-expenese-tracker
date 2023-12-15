<template>
  <h3>Add new transaction</h3>
  <form id="form" @submit.prevent="onSubmit">
    <div class="form-control">
      <label for="text">Text</label>
      <input type="text" id="text" v-model="text" placeholder="Enter text..." />
    </div>
    <div class="form-control">
      <label for="amount"
        >Amount <br />
        (negative - expense, positive - income)</label
      >
      <input
        type="number"
        id="amount"
        v-model="amount"
        placeholder="Enter amount..."
      />
    </div>
    <button class="btn">Add transaction</button>
  </form>
</template>

<script setup lang="ts">
import { ref } from "vue";
import { useToast } from "vue-toastification";
import type { Transaction } from "../types";
const text = ref("");
const amount = ref(0);
let newTransaction = ref<Transaction>({
  id: 0,
  text: "",
  amount: 0,
});
const emit = defineEmits(["addTransactionSuccess"]);
const toast = useToast();

const onSubmit = () => {
  if (text.value.trim() === "" || amount.value === 0) {
    toast.error("Please add a text and amount");
    return;
  }

  newTransaction.value = {
    id: Math.floor(Math.random() * 100000000),
    text: text.value,
    amount: +amount.value,
  };

  emit("addTransactionSuccess", newTransaction.value);

  text.value = "";
  amount.value = 0;
};
</script>

<style scoped></style>
