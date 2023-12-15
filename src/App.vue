<template>
  <Header></Header>
  <Balance :balance="balance"></Balance>
  <IncomeExpenses
    :total-income="getTotalIncome"
    :total-expense="getTotalExpense"
  ></IncomeExpenses>
  <TransactionList
    :transactions="transactions"
    @deleteTransactionSuccess="handleDeleteTransactionSuccess"
  ></TransactionList>
  <AddTransaction
    @addTransactionSuccess="handleAddTransactionSuccess"
  ></AddTransaction>
</template>

<script setup lang="ts">
import Header from "./components/Header.vue";
import Balance from "./components/Balance.vue";
import IncomeExpenses from "./components/IncomeExpenses.vue";
import TransactionList from "./components/TransactionList.vue";
import AddTransaction from "./components/AddTransaction.vue";

import type { Transaction } from "./types";
import { useToast } from "vue-toastification";
import { ref, computed, onMounted } from "vue";

const toast = useToast();
const transactions = ref<Transaction[]>([]);

onMounted(() => {
  // const res = await fetch("http://localhost:5000/transactions").catch((err) => {
  //   toast.error(err.message);
  // });
  // if (!res) return;
  // transactions.value = await res.json();
});
const transactionsFromLocalStorage = localStorage.getItem("transactions");
if (transactionsFromLocalStorage) {
  transactions.value = JSON.parse(
    transactionsFromLocalStorage
  ) as Transaction[];
  toast.success("Transactions loaded!");
}

const balance = computed(() => {
  return transactions.value.reduce((acc, transaction) => {
    return acc + transaction.amount;
  }, 0);
});

const getTotalIncome = computed(() => {
  return transactions.value
    .filter((transaction) => transaction.amount > 0)
    .reduce((acc, transaction) => {
      return acc + transaction.amount;
    }, 0);
});

const getTotalExpense = computed(() => {
  return transactions.value
    .filter((transaction) => transaction.amount < 0)
    .reduce((acc, transaction) => {
      return acc + transaction.amount;
    }, 0);
});

const handleAddTransactionSuccess = (transaction: Transaction) => {
  transactions.value.push(transaction);
  toast.success("Transaction added");
  saveTransactionsToLocalStorage();
};

const handleDeleteTransactionSuccess = (id: number) => {
  transactions.value = transactions.value.filter(
    (transaction) => transaction.id !== id
  );
  toast.success("Transaction deleted!");
  saveTransactionsToLocalStorage();
};

const saveTransactionsToLocalStorage = () => {
  localStorage.setItem("transactions", JSON.stringify(transactions.value));
};
</script>

<style scoped></style>
