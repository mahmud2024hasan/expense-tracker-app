<script setup>
import { ref, computed } from "vue";

const props = defineProps(["transactions"]);
const emit = defineEmits(["delete"]);

const filter = ref("all");

// Filtered Transaction List
const filteredTransactions = computed(() => {
  if (filter.value === "income") {
    return props.transactions.filter((t) => t.type === "INCOME");
  } else if (filter.value === "expense") {
    return props.transactions.filter((t) => t.type === "EXPENSE");
  }
  return props.transactions;
});
</script>

<template>
  <div class="container">
    <div class="header">
      <div class="filter-area">
        <div class="radio-group">
          <label><input type="radio" v-model="filter" value="all" /> All</label>
          <label><input type="radio" v-model="filter" value="income" />Income</label>
          <label><input type="radio" v-model="filter" value="expense" />Expense</label>
        </div>
      </div>
    </div>
    <div class="table">
      <table class="transactions">
        <thead>
          <tr>
            <th>Title</th>
            <th>Amount</th>
            <th>Type</th>
            <th>Action</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(transaction, index) in filteredTransactions" :key="index">
            <td>{{ transaction.title }}</td>
            <td
              :class="{
                'text-success': transaction.type === 'INCOME',
                'text-danger': transaction.type === 'EXPENSE',
                'fw-bold': transaction.type === 'EXPENSE' && transaction.amount >= 500
              }"
            >
              $ {{ transaction.amount }}
            </td>
            <td class="text-uppercase">{{ transaction.type }}</td>
            <td>
              <button class="delete-button" @click="emit('delete', index)">Delete</button>
            </td>
          </tr>
          <tr v-if="filteredTransactions.length === 0">
            <td colspan="4" class="text-center">No transactions recorded yet.</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<style scoped>

.header {
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.transactions {
  width: 100%;
  table-layout: fixed;
  border-collapse: collapse;
  margin: 10px 0;
  font-family: Arial, sans-serif;
}

.transactions th,
.transactions td {
  border: 1px solid #ddd;
  padding: 12px;
  text-align: center;
  width: 25%;
}

.transactions th {
  background-color: #f4f4f4;
  font-weight: bold;
  color: #333;
}

.transactions tr:hover {
  background-color: #f9f9f9;
}

.delete-button {
  background-color: #e40808;
  color: white;
  border: none;
  padding: 10px 20px;
  font-size: 16px;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

button:hover {
  background-color: #b30000;
}

.text-success{
  color: rgb(1, 117, 1);
}

.text-danger{
  color: #d32700;
}

.text-uppercase{
  text-transform: uppercase;
}

.fw-bold{
  font-weight: bold;
}

.radio-group {
  display: flex;
  gap: 16px; 
}

.radio-group label {
  display: flex;
  align-items: center;
  gap: 3px; 
  cursor: pointer;
}

</style>
