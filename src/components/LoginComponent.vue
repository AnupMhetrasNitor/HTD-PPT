<!-- src/components/LoginComponent.vue -->
<template>
  <div class="login">
    <h2>Login</h2>
    <form @submit.prevent="loginUser">
      <div>
        <label for="username">Username:</label>
        <input v-model="form.userName" type="text" id="username" required />
      </div>
      <div>
        <label for="password">Password:</label>
        <input v-model="form.password" type="password" id="password" required />
      </div>
      <button type="submit">Login</button>
      <router-link to="/register">New User Register Here</router-link>
    </form>
    <p v-if="errorMessage" class="error">{{ errorMessage }}</p>
  </div>
</template>

<script>
import axios from 'axios';
import { mapActions } from 'vuex';

export default {
  data() {
    return {
      form:{
        userName: '',
      password: '',
      }
     
    };
  },
  methods: {
    ...mapActions(['fetchUser']),
    
    async loginUser() {
  try {
    console.log('Login request initiated with:');
    console.log('Username:', this.form.userName);
    console.log('Password:', this.form.password);

    
    // const requestUrl = `http://localhost:8080/api/users/login,${this.username,this.password}`;
    // console.log('Request URL:', requestUrl);
    
    
    const response = await axios.post('http://localhost:8080/api/users/login',this.form);
    
   
    console.log('Response:', response);
    this.$store.commit('SET_USER', response.data);
    this.$router.push({ name: 'expenseList' }); 
  } catch (error) {
    console.error('Error occurred:', error);
    this.errorMessage = 'Invalid credentials. Please try again.';
  }
}

  }
};

</script>
<style scoped>

.login {
  max-width: 450px;
  margin: 80px auto;
  padding: 40px;
  border-radius: 12px;
  background-color: #F0F8FF; /* Soft light blue background */
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.1);
  text-align: center;
}

/* Heading Styling */
h2 {
  color: #2E4053; /* Dark Slate Blue */
  font-size: 32px;
  font-weight: bold;
  margin-bottom: 30px;
}

/* Form Styling */
form {
  display: flex;
  flex-direction: column;
  gap: 20px;
}

/* Label and Input Fields Styling */
label {
  font-size: 16px;
  font-weight: 600;
  color: #5D6D7E; /* Greyish Blue */
  margin-bottom: 8px;
  text-align: left;
}

input {
  padding: 12px;
  border: 1px solid #A9CCE3; /* Light Blue Border */
  border-radius: 8px;
  font-size: 16px;
  color: #34495E; /* Darker Grey */
  background-color: #ECF0F1; /* Very light grey background */
  transition: border-color 0.3s ease, box-shadow 0.3s ease;
}

input:focus {
  border-color: #3498DB; /* Vibrant Blue on Focus */
  box-shadow: 0 0 5px rgba(52, 152, 219, 0.5); /* Light Blue Glow */
  outline: none;
}

/* Button Styling */
button {
  padding: 12px;
  background-color: #3498DB; /* Vibrant Blue */
  color: white;
  font-size: 16px;
  font-weight: 600;
  border: none;
  border-radius: 8px;
  cursor: pointer;
  transition: background-color 0.3s ease, transform 0.2s ease;
}

button:hover {
  background-color: #2980B9; /* Darker Blue */
  transform: translateY(-2px);
}

button:focus {
  outline: none;
}

/* Register Link Styling */
.register-link {
  color: #3498DB; /* Same Vibrant Blue */
  font-size: 14px;
  text-decoration: none;
  margin-top: 15px;
}

.register-link:hover {
  text-decoration: underline;
}

/* Error Message Styling */
.error {
  color: #E74C3C; /* Red */
  text-align: center;
  margin-top: 15px;
  font-size: 14px;
  font-weight: 600;
}

</style>