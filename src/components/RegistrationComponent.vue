<template>
    <div class="register-form">
      <h2>Register</h2>
      <form @submit.prevent="registerUser">
       
        <div>
          <label for="name">Username:</label>
          <input type="text" id="name" v-model="form.userName" required />
        </div>
  
        <div>
          <label for="phone">Phone Number:</label>
          <input type="tel" id="phone" v-model="form.phoneNumber" required />
        </div>
  
        <div>
          <label for="email">Email:</label>
          <input type="email" id="email" v-model="form.email" required />
        </div>
  
        <div>
          <label for="password">Password:</label>
          <input type="password" id="password" v-model="form.password" required />
        </div>
  
        <button type="submit">Register</button>
      </form>
    </div>
  </template>
  
  <script>
  import router from '@/router';
import axios from 'axios';
  
  export default {
    name: "RegisterForm",
    data() {
      return {
        form: {
          userName: "",
          phoneNumber: "",
          email: "",
          password: "",
        },
      };
    },
    methods: {
      async registerUser() {
        try {
          const response = await axios.post("http://localhost:8080/api/users", this.form);
          alert("Registration Successful!");
          console.log(response.data);
          router.push("/")
        } catch (error) {
          console.error("Error while registering user:", error);
          alert("Registration failed. Please try again.");
        }
      },
    },
  };
  </script>
  <style scoped>
  /* Container for the form */
  .register-form {
    max-width: 450px;
    margin: 60px auto;
    padding: 30px;
    border-radius: 10px;
    background-color: #fff;
    box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
  }
  
  /* Heading Style */
  h2 {
    text-align: center;
    font-size: 28px;
    font-weight: bold;
    color: #333;
    margin-bottom: 30px;
  }
  
  /* Form Layout */
  form {
    display: flex;
    flex-direction: column;
  }
  
  /* Input Field Styles */
  div {
    margin-bottom: 20px;
  }
  
  label {
    font-size: 16px;
    font-weight: 600;
    color: #555;
    margin-bottom: 8px;
  }
  
  input {
    padding: 12px;
    font-size: 16px;
    border: 1px solid #ddd;
    border-radius: 8px;
    background-color: #f9f9f9;
    transition: border-color 0.3s ease;
  }
  
  input:focus {
    border-color: #007bff;
    outline: none;
  }
  
  /* Button Styles */
  button {
    padding: 14px;
    background-color: #28a745;
    color: white;
    font-size: 16px;
    font-weight: bold;
    border: none;
    border-radius: 8px;
    cursor: pointer;
    transition: background-color 0.3s ease;
  }
  
  button:hover {
    background-color: #218838;
  }
  
  button:focus {
    outline: none;
  }
  
  /* Additional Styling */
  .error {
    color: red;
    text-align: center;
    margin-top: 20px;
    font-size: 14px;
  }
  
  /* Make inputs and buttons full width */
  input, button {
    width: 100%;
  }
  
  /* For mobile responsiveness */
  @media (max-width: 480px) {
    .register-form {
      padding: 20px;
      margin: 20px;
    }
  
    h2 {
      font-size: 24px;
    }
  }
  </style>