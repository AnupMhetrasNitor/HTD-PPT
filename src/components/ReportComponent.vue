<!-- src/components/ReportComponent.vue -->
<template>
  <div class="report">
    <h2>Expense Report</h2>
    <p>Total Expenses: ${{ totalExpenses }}</p>
    <div>
      <h3>Expenses by Category</h3>
      <ul>
        <li v-for="(total, category) in expensesByCategory" :key="category">
          {{ category }}: ${{ total }}
        </li>
      </ul>
    </div>
    <!-- Optionally, integrate charts here -->
  </div>
</template>

<script>
import { mapGetters } from 'vuex';

export default {
  computed: {
    ...mapGetters(['totalExpenses', 'expensesByCategory']),
  },
};
</script>

<style scoped>
/* General Container for Report */
.report {
  max-width: 600px;
  margin: 40px auto;
  padding: 25px;
  background-color: #fff;
  border-radius: 10px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
  color: #333;
}

/* Heading for the report */
h2 {
  text-align: center;
  font-size: 32px;
  font-weight: bold;
  color: #2c3e50;
  margin-bottom: 20px;
}

/* Total Expenses Styling */
.total-expenses {
  font-size: 20px;
  font-weight: 600;
  color: #e74c3c; /* A red color for emphasis */
  text-align: center;
  margin-bottom: 40px;
}

/* Section for Expenses by Category */
.category-expenses {
  margin-bottom: 20px;
}

h3 {
  font-size: 24px;
  color: #34495e;
  margin-bottom: 15px;
}

/* Category List Styling */
ul {
  list-style-type: none;
  padding-left: 0;
}

li {
  display: flex;
  justify-content: space-between;
  padding: 10px;
  border-bottom: 1px solid #f0f0f0;
}

li:last-child {
  border-bottom: none;
}

/* Category Name Styling */
.category-name {
  font-size: 18px;
  font-weight: 500;
  color: #34495e;
}

/* Category Total Styling */
.category-total {
  font-size: 18px;
  font-weight: 600;
  color: #27ae60; /* A green color for totals */
}

/* For Mobile Devices */
@media (max-width: 480px) {
  .report {
    padding: 20px;
    margin: 20px;
  }

  h2 {
    font-size: 28px;
  }

  .total-expenses {
    font-size: 18px;
  }

  .category-name,
  .category-total {
    font-size: 16px;
  }
}
</style>