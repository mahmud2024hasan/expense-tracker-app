<script setup>
import { ref } from "vue";

const emit = defineEmits(["add"]);

const title = ref("");
const amount = ref("");
const type = ref("");

const error = ref("");

// Function for add new transaction
const addTransaction = () => {
  // Error handling
  if (!title.value || !amount.value || !type.value) {
    error.value = "All fields are required!";
    return;
  }
  if (amount.value <= 0) {
    error.value = "Amount must be greater than 0 and not a negative number!";
    return;
  }

  // Add new transaction
  const newTransaction = {
    title: title.value,
    amount: parseFloat(amount.value),
    type: type.value.toUpperCase(),
  };

  // Send transaction
  emit("add", newTransaction);

  // Form reset after submit
  title.value = "";
  amount.value = "";
  type.value = "";
  error.value = "";
};
</script>

<template>
  <div class="container">
    <div v-if="error" class="error-msg">{{ error }}</div>

    <div class="transaction-form">
      <div class="form-input">
        <label for="title">Title:</label>
        <input type="text" v-model="title" placeholder="Transaction Title" />
      </div>
      <div class="form-input">
        <label for="amount">Amount:</label>
        <input
          type="number"
          v-model="amount"
          placeholder="Transaction Amount"
        />
      </div>
      <div class="form-input">
        <label for="type">Type:</label>
        <select v-model="type">
          <option value="" disabled selected>Transaction Type</option>
          <option value="income">Income</option>
          <option value="expense">Expense</option>
        </select>
      </div>
      <div class="form-input">
        <button class="btn btn-primary" @click="addTransaction">
          Add Transaction
        </button>
      </div>
    </div>
  </div>
</template>

<style scoped>
.transaction-form {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  align-items: flex-end;
  gap: 16px;
  width: 100%;
  flex-wrap: wrap;
  margin-bottom: 20px;
}

.form-input {
  display: flex;
  flex-direction: column;
  justify-content: center;
  margin-bottom: 15px;
}

.form-input label {
  margin-bottom: 5px;
  text-align: left;
}

.form-input input,
.form-input select {
  padding: 8px;
  border: 1px solid #ccc;
  border-radius: 4px;
  font-size: 16px;
}

.form-input input:focus,
.form-input select:focus {
  border-color: #66afe9;
  box-shadow: 0 0 5px rgba(102, 175, 233, 0.5);
  outline: none;
}

button {
  background: #0d6bf7;
  color: white;
  border: none;
  cursor: pointer;
  padding: 10px;
  font-size: 16px;
  border-radius: 4px;
}

button:hover {
  background: #0b5ed7;
}

.error-msg {
  width: 100%;
  padding: 10px;
  font-size: 18px;
  color: #fff;
  background-color: #e988a2;
  border-radius: 5px;
  margin-bottom: 20px;
}
</style>
