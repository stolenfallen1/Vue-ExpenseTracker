<template>
  <div>
    <Header />
    <div class="container">
      <Balance :total="total" />
      <IncomeExpense :income="income" :expenses="expenses" />
      <TransactionList
        :transactions="transactions"
        @deleteTransaction="handleTransactionDeleted"
      />
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

import { ref, computed, onMounted } from "vue";

// Get transaction data from local storage on page load / mount
onMounted(() => {
  const savedTransactions = JSON.parse(localStorage.getItem("transactions"));
  if (savedTransactions) {
    transactions.value = savedTransactions;
  }
});

const toast = useToast();

const transactions = ref([]);

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
  savedTransactionsToLocalStorage();
  toast.success("Transaction added successfully");
};

// Delete transaction
const handleTransactionDeleted = (id) => {
  transactions.value = transactions.value.filter(
    (transaction) => transaction.id !== id
  );
  savedTransactionsToLocalStorage();
  toast.success("Transaction deleted");
};

// Save transaction data to local storage
const savedTransactionsToLocalStorage = () => {
  localStorage.setItem("transactions", JSON.stringify(transactions.value));
};
</script>

<style lang="scss" scoped></style>
