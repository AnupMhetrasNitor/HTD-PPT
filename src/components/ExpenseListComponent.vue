<template>
  <div class="expense-list">
    <h2>Expenses</h2>
    <div>
      <label for="categoryFilter">Category:</label>
      <select v-model="categoryFilter" @change="filterExpenses">
        <option value="">All</option>
        <option value="FOOD">Food</option>
        <option value="TRANSPORT">Transport</option>
        <option value="ENTERTAINMENT">Entertainment</option>
        <option value="MISCELLANEOUS">MISCELLANEOUS</option>
        <option value="UTILITIES"></option>
        <!-- Add other categories as needed -->
      </select>
    </div>

    <ul>
      <li v-for="expense in filteredExpenses" :key="expense.id">
        <p>*
          {{ expense.title }} - ${{ expense.amount }} ({{ expense.category }})</p>
        <button @click="deleteExpense(expense.id)">Delete</button>
        <button @click="editExpense(expense)">Edit</button>
      </li>
    </ul>
  </div>
</template>

<script>
import { mapState, mapActions } from 'vuex';

export default {
  data() {
    return {
      categoryFilter: '',
    };
  },
  computed: {
    ...mapState(['expenses']),
    filteredExpenses() {
      if (this.categoryFilter) {
        return this.expenses.filter(expense => expense.category === this.categoryFilter);
      }
      return this.expenses;
    }
  },
  methods: {
    ...mapActions(['fetchExpenses', 'deleteExpense']),
    
    async deleteExpense(expenseId) {
      await this.$store.dispatch('deleteExpense',expenseId)
    },
    
    editExpense(expense) {
      // Redirect to edit page or open edit form with existing expense details
      this.$router.push({ name: 'editExpense', params: { id: expense.id } });
    },
  },
  mounted() {
    this.fetchExpenses();
  }
};
</script>

<style scoped>
/* General Container Styling */
.expense-list {
  max-width: 700px; 
  margin: 30px auto;
  padding: 25px;
  border-radius: 12px;
  background-color: #ffffff;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
}

/* Heading */
h2 {
  text-align: center;
  font-size: 28px;
  color: black;
  font-weight: bold;
  margin-bottom: 30px;
}

/* Filter Container */
.filter-container {
  display: flex;
  justify-content: flex-start;
  align-items: center;
  margin-bottom: 20px;
}

label {
  font-size: 16px;
  font-weight: 600;
  color: #333;
  margin-right: 15px;
}

select {
  padding: 10px;
  font-size: 16px;
  border-radius: 6px;
  border: 1px solid #ddd;
  background-color: #f7f7f7;
  transition: border-color 0.3s ease;
}

select:focus {
  border-color: black;
  outline: none;
}

/* Expense List */
ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 15px;
  border-bottom: 1px solid #f0f0f0;
  font-size: 16px;
}

li:last-child {
  border-bottom: none;
}

/* Expense Information */
.expense-info p {
  margin: 0;
  color: #555;
}

.amount {
  color: #4CAF50;
  font-weight: 600;
}

/* Expense Actions (Buttons) */
.expense-actions {
  display: flex;
  gap: 10px;
}

button {
  padding: 8px 14px;
  border: none;
  border-radius: 8px;
  font-size: 14px;
  font-weight: 600;
  cursor: pointer;
  transition: background-color 0.3s ease, color 0.3s ease;
}

button:first-child {
  background-color: #007bff;
  color: white;
}

button:first-child:hover {
  background-color: #0056b3;
}

button:first-child:focus {
  outline: none;
}

button:last-child {
  background-color: #e74c3c;
  color: white;
}

button:last-child:hover {
  background-color: #c0392b;
}

button:last-child:focus {
  outline: none;
}

/* Responsive Design */
@media (max-width: 480px) {
  .expense-list {
    padding: 15px;
  }

  h2 {
    font-size: 24px;
  }

  select {
    font-size: 14px;
    padding: 8px;
  }

  li {
    padding: 12px;
    font-size: 14px;
  }

  button {
    font-size: 12px;
    padding: 6px 10px;
  }
}
</style>
