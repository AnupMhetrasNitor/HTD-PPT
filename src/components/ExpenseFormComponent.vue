<template>
  <div class="add-expense-form">
    <h2>Add Expense</h2>
    <form @submit.prevent="submitExpenseForm">
      <div class="form-group">
        <label for="title">Title:</label>
        <input type="text" id="title" v-model="expense.title" required />
      </div>

      <div class="form-group">
        <label for="amount">Amount:</label>
        <input type="number" id="amount" v-model="expense.amount" required min="0" step="0.01" />
      </div>

      <div class="form-group">
        <label for="category">Category:</label>
        <select id="category" v-model="expense.category" required>
          <option value="FOOD">Food</option>
          <option value="TRANSPORT">Transport</option>
          <option value="ENTERTAINMENT">Entertainment</option>
          <option value="OTHER">Other</option>
        </select>
      </div>

      <div class="form-group">
        <label for="date">Date:</label>
        <input type="date" id="date" v-model="expense.date" required />
      </div>

      <button type="submit">Add Expense</button>
    </form>
  </div>
</template>

<script>
import { mapState, mapActions } from 'vuex';

export default {
  name: 'AddExpenseForm',
  data() {
    return {
      expense: {
        title: '',
        amount: 0,
        category: 'FOOD', // Default category
        date: '',
      },
    };
  },
  computed: {
    // Get user data from Vuex store
    ...mapState(['user']),
  },
  methods: {
    ...mapActions(['addExpense']), // Map the addExpense action from Vuex
    async submitExpenseForm() {
      // Check if user data is available
      if (!this.user || !this.user.id) {
        alert('You must be logged in to add an expense.');
        return;
      }

      console.log("Form data: ",this.expense);
      

      
      const expenseData = {
        ...this.expense,
        userId: this.user.id, // Assign the user ID from Vuex store
      };

      // Call the Vuex action to add the expense
      const response = await this.addExpense(expenseData);

      console.log("Added expense: ",response );
      

      
      this.$router.push('/dashboard');

      console.log("Form submitted");
      
    },
  },
};
</script>
<style scoped>
/* General Form Styling */
.add-expense-form {
  max-width: 480px;
  margin: 40px auto;
  padding: 30px;
  border-radius: 10px;
  background-color: #fff;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
}

h2 {
  text-align: center;
  color: black;
  font-size: 26px;
  font-weight: bold;
  margin-bottom: 30px;
}

.form-group {
  margin-bottom: 18px;
}

label {
  display: block;
  margin-bottom: 8px;
  font-size: 14px;
  font-weight: 600;
  color: #333;
}

input,
select {
  width: 100%;
  padding: 12px;
  font-size: 16px;
  border: 2px solid #ddd;
  border-radius: 8px;
  background-color: #f4f7fa;
  color: #333;
  transition: border-color 0.3s;
}

input:focus,
select:focus {
  border-color: #4CAF50;
  outline: none;
}

input[type="number"]::-webkit-outer-spin-button,
input[type="number"]::-webkit-inner-spin-button {
  -webkit-appearance: none;
  margin: 0;
}

button {
  width: 100%;
  padding: 14px;
  background-color: #ee194b;
  color: white;
  border: none;
  border-radius: 8px;
  font-size: 18px;
  font-weight: 600;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

button:hover {
  background-color: #bce854;
}

button:active {
  background-color: #bce854;
}

/* Mobile Friendly */
@media (max-width: 480px) {
  .add-expense-form {
    padding: 20px;
  }
  
  h2 {
    font-size: 22px;
  }
}
</style>
