<template>
  <div id="app">
    <nav v-if="user">
      <ul class="navbar">
        <li><router-link to="/dashboard">Expense List</router-link></li>
        <li><router-link to="/expenses/add">Add an Expense</router-link></li>
        <li><router-link to="/report">Report</router-link></li>
        <li class="logout"><button @click="logout">Logout</button></li>
      </ul>
    </nav>
    
    <router-view></router-view>
  </div>
</template>

<script>
export default {
  computed: {
    user() {
      return this.$store.state.user;
    },
  },

  methods: {
    logout() {
      this.$store.commit('SET_USER', null); // Clear user data from Vuex
      this.$router.push({ name: 'login' }); // Redirect to login page
    },
  },
};
</script>

<style scoped>
/* Base Styles */
#app {
  font-family: 'Arial', sans-serif;
  text-align: center;
  color: #2c3e50; /* Dark Gray */
  background-color: #ecf0f1; /* Light Gray */
  min-height: 100vh;
  padding: 20px;
}

/* Navigation Styling */
nav {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  padding: 10px 20px;
  background-color: #34495e; /* Dark Blue */
  /* border-radius: 8px; */
  z-index: 10; /* Ensure navbar is above other content */
}

.navbar {
  list-style-type: none;
  padding: 0;
  margin: 0;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.navbar li {
  display: inline-block;
}

.navbar li a,
.navbar li button {
  color: #ecf0f1; /* Light Gray */
  font-weight: 600;
  text-decoration: none;
  padding: 12px 24px;
  background-color: transparent;
  border: 2px solid transparent;
  border-radius: 8px;
  transition: background-color 0.3s, border-color 0.3s, transform 0.3s;
}

.navbar li button {
  background-color: #2c3e50;
}

.navbar li a:hover,
.navbar li button:hover {
  background-color: #1abc9c; /* Vibrant Green */
  border-color: #1abc9c; /* Vibrant Green */
  transform: translateY(-2px); /* Slight elevation on hover */
}

/* Active Link Styling */
nav a.router-link-exact-active {
  color: #f39c12; /* Yellow-Orange for active link */
  font-weight: bold;
}

/* Button Styling */
button {
  cursor: pointer;
  transition: background-color 0.3s ease, transform 0.2s ease;
}

button:hover {
  background-color: #e74c3c; /* Red background on hover */
  transform: scale(1.05);
}

button:focus {
  outline: none;
}

/* Adjustments for navbar layout */
.navbar .logout {
  margin-left: auto; /* Push logout button to the right */
}

/* General layout improvements */
router-view {
  margin-top: 80px; /* Adjust content so it doesn't overlap the fixed navbar */
}
</style>
