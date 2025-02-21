# Ostad Module 24 Assignment : Expense Tracker App Using Vue.js

## Project Setup :
• Create a new Vue project using Vite.

• Name the project expense-tracker-app.

• Install Bootstrap for styling (optional), but the final output must use a table. (NB: Do not use any DataTable package; the table should be implemented manually.)


## Component Architecture :
#### 1. TransactionList.vue
• Displays the list of transactions in a table.
• Allows filtering transactions by income, expense, or all.
• Provides a delete button for each transaction.
• location: src/components/TransactionList.vue

#### 2. AddTransaction.vue
• Contains a form to add new transactions with fields:
1. Title (text)
2. Amount (number)
3. Type (dropdown: Income / Expense)
• Shows validation messages if inputs are invalid.
• location: src/components/AddTransaction.vue

## Data and State Management :
• Store transactions in a reactive state inside a ref().
• Load transactions from localStorage when the app starts.
• Save transactions to localStorage when a new one is added or deleted.

## Style Binding :
• Use Bootstrap table styles or a similar framework.
• Apply text colors dynamically:
1. Green for Income
2. Red for Expense
3. Bold for expenses above or equal $500
4. Type should be uppercase.

## Conditional Rendering :
• If no transactions exist, display: "No transactions recorded yet."

## List Rendering & Filters :
• Display transactions in a table using v-for.
• Implement a filter to show only:
1. All transactions
2. Income transactions
3. Expense transactions

## JavaScript Logic & Validation :
• Amount must be greater than 0 and not a negative number.

## Dynamic Event Handling :
• Clicking "Add" should create a new transaction.
• Clicking "Delete" should remove a transaction and update localStorage.

## Persistent Data :
• Store transactions in localStorage to persist after a page reload.
• When deleting a transaction, update localStorage.
