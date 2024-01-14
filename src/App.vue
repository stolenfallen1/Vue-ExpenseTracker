<template>
  <div>
    <Header />
    <div class="container">
      <Balance />
      <IncomeExpense />
      <TransactionList :transactions="transactions" />
      <AddTransaction />
    </div>
  </div>
</template>

<script setup>
import AddTransaction from "./components/AddTransaction.vue";
import TransactionList from "./components/TransactionList.vue";
import IncomeExpense from "./components/IncomeExpense.vue";
import Balance from "./components/Balance.vue";
import Header from "./components/Header.vue";

import { ref } from "vue";

const transactions = ref([
  { id: 1, text: "Flower", amount: -19.99 },
  { id: 2, text: "Salary", amount: 299.97 },
  { id: 3, text: "Book", amount: -10 },
  { id: 4, text: "Camera", amount: 150 },
]);
</script>

<style lang="scss" scoped></style>
