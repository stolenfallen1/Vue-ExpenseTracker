<template>
  <div>
    <Header />
    <div class="container">
      <Balance :total="total" />
      <IncomeExpense :income="income" :expenses="expenses" />
      <TransactionList :transactions="transactions" />
      <AddTransaction @addTransaction="handleTransactionSubmitted" />
    </div>
  </div>
</template>

<script setup>
import { useToast } from "vue-toastification";

import AddTransaction from "./components/AddTransaction.vue";
import TransactionList from "./components/TransactionList.vue";
import IncomeExpense from "./components/IncomeExpense.vue";
import Balance from "./components/Balance.vue";
import Header from "./components/Header.vue";

import { ref, computed } from "vue";

const transactions = ref([
  { id: 1, text: "Flower", amount: -19.99 },
  { id: 2, text: "Salary", amount: 299.97 },
  { id: 3, text: "Book", amount: -10 },
  { id: 4, text: "Camera", amount: 150 },
]);

const toast = useToast();

// Get total amount of transactions
const total = computed(() => {
  return transactions.value.reduce((acc, transaction) => {
    return acc + transaction.amount;
  }, 0);
});

// Get income
const income = computed(() => {
  return transactions.value
    .filter((transaction) => transaction.amount > 0)
    .reduce((acc, transaction) => {
      return acc + transaction.amount;
    }, 0);
});

// Get expense
const expenses = computed(() => {
  return transactions.value
    .filter((transaction) => transaction.amount < 0)
    .reduce((acc, transaction) => {
      return acc + transaction.amount;
    }, 0);
});

// Add transaction
const handleTransactionSubmitted = (transactionData) => {
  transactions.value.push({
    id: Math.floor(Math.random() * 100000000), // Not to be used in production
    text: transactionData.text,
    amount: transactionData.amount,
  });
  toast.success("Transaction added successfully");
};
</script>

<style lang="scss" scoped></style>
