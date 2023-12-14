<template>
  <Header></Header>
  <Balance></Balance>
  <IncomeExpenses></IncomeExpenses>
  <TransactionList></TransactionList> 
</template>

<script setup lang="ts">
import Header from "./components/Header.vue";
import Balance from "./components/Balance.vue";
import IncomeExpenses from "./components/IncomeExpenses.vue";
import TransactionList from "./components/TransactionList.vue";
import AddTransaction from "./components/AddTransaction.vue";
</script>

<style scoped></style>
