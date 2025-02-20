<script setup>
import { ref, onMounted, watch } from "vue";
import TransactionList from "./components/TransactionList.vue";
import AddTransaction from "./components/AddTransaction.vue";

const transactions = ref([]);

// Transaction load from local storage
onMounted(() => {
  const savedTransactions = localStorage.getItem("transactions");
  if (savedTransactions) {
    transactions.value = JSON.parse(savedTransactions);
  }
});

// Save data in local storage
watch(transactions, (newVal) => {
  localStorage.setItem("transactions", JSON.stringify(newVal));
}, { deep: true });

// Function to add new transaction
const addTransaction = (transaction) => {
  transactions.value.push(transaction);
};

// Delete transaction
const deleteTransaction = (index) => {
  transactions.value.splice(index, 1);
};
</script>

<template>

  <div class="container">
    
    <div class="heading">
      <h1>Expense Tracker</h1>
    </div>

    <main>
      <!-- Transaction Form-->
      <AddTransaction @add="addTransaction" />

      <!-- Transaction Table -->
      <TransactionList :transactions="transactions" @delete="deleteTransaction" />
    </main>

  </div>

</template>

<style scoped>

    .container {
      width: 800px;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      margin: 0 auto;
      text-align: center;
    }

    .heading {
      margin-top: 70px;
      margin-bottom: 20px;
    }

    main {
      width: 100%;
    }
</style>
