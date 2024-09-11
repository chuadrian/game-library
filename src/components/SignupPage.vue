<!-- SignupPage.vue -->
<template>
    <div class="signup-overlay">
      <div class="auth-container">
        <button class="close-button" @click="$emit('close')">&times;</button>
        <div class="form-switcher">
          <button
            :class="{'active': isSignup}"
            @click="isSignup = true"
          >
            Sign Up
          </button>
          <button
            :class="{'active': !isSignup}"
            @click="isSignup = false"
          >
            Log In
          </button>
        </div>
    
        <transition name="cyber-slide">
          <div v-if="isSignup" key="signup" class="form-container signup-container">
            <h2>Sign Up</h2>
            <form @submit.prevent="handleSubmit" class="signup-form">
              <div class="form-group">
                <label for="username">Username:</label>
                <input
                  type="text"
                  id="username"
                  v-model="username"
                  required
                  class="form-input"
                />
              </div>
              <div class="form-group">
                <label for="email">Email:</label>
                <input
                  type="email"
                  id="email"
                  v-model="email"
                  required
                  class="form-input"
                />
              </div>
              <div class="form-group">
                <label for="password">Password:</label>
                <input
                  type="password"
                  id="password"
                  v-model="password"
                  required
                  class="form-input"
                />
              </div>
              <div class="form-group">
                <label for="confirmPassword">Confirm Password:</label>
                <input
                  type="password"
                  id="confirmPassword"
                  v-model="confirmPassword"
                  required
                  class="form-input"
                />
              </div>
              <button type="submit" class="submit-button">Sign Up</button>
            </form>
          </div>
          <div v-else key="login" class="form-container login-container">
            <h2>Log In</h2>
            <form @submit.prevent="handleLogin" class="login-form">
              <div class="form-group">
                <label for="loginEmail">Email:</label>
                <input
                  type="email"
                  id="loginEmail"
                  v-model="loginEmail"
                  required
                  class="form-input"
                />
              </div>
              <div class="form-group">
                <label for="loginPassword">Password:</label>
                <input
                  type="password"
                  id="loginPassword"
                  v-model="loginPassword"
                  required
                  class="form-input"
                />
              </div>
              <button type="submit" class="submit-button">Log In</button>
            </form>
          </div>
        </transition>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    name: 'SignupPage',
    emits: ['close'],
    data() {
      return {
        isSignup: true,
        username: '',
        email: '',
        password: '',
        confirmPassword: '',
        loginEmail: '',
        loginPassword: ''
      }
    },
    methods: {
      handleSubmit() {
        if (this.password !== this.confirmPassword) {
          alert('Passwords do not match');
          return;
        }
        console.log('Signup submitted', {
          username: this.username,
          email: this.email,
          password: this.password
        });
        this.$emit('close');
        this.resetForm();
      },
      handleLogin() {
        console.log('Login submitted', {
          email: this.loginEmail,
          password: this.loginPassword
        });
        this.$emit('close');
        this.resetForm();
      },
      resetForm() {
        this.username = '';
        this.email = '';
        this.password = '';
        this.confirmPassword = '';
        this.loginEmail = '';
        this.loginPassword = '';
      }
    }
  }
  </script>
  
  <style scoped>

@import url('https://fonts.googleapis.com/css2?family=Orbitron:wght@400..900&display=swap');
*{
    font-family: "Orbitron", sans-serif;
}
  .signup-overlay {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.5);
    display: flex;
    justify-content: center;
    align-items: center;
    z-index: 1000;
  }
  
  .auth-container {
    position: relative;
    max-width: 600px;
    width: 100%;
    padding: 30px;
    background: linear-gradient(135deg, #1e1e2f 0%, #2d2d4a 100%);
    border-radius: 15px;
    box-shadow: 0 15px 30px rgba(0, 0, 0, 0.5);
    border: 2px solid #00ffcc;
    z-index: 1001;
    overflow: hidden;
  }
  
  .close-button {
    position: absolute;
    top: 5px;
    right: 10px;
    background: none;
    border: none;
    color: #00ffcc;
    font-size: 24px;
    cursor: pointer;
    transition: color 0.3s ease;
  }
  
  .close-button:hover {
    color: #00d4ff;
  }
  
  h2 {
    text-align: center;
    color: #00ffcc;
    font-family: 'Orbitron', sans-serif;
    margin-bottom: 15px;
    font-size: 24px;
    text-transform: uppercase;
  }
  
  .form-switcher {
    display: flex;
    justify-content: center;
    margin-bottom: 10px;
  }
  
  .form-switcher button {
    background: transparent;
    border: none;
    color: #00ffcc;
    font-size: 18px;
    padding: 10px;
    cursor: pointer;
    transition: all 0.3s ease;
  }
  
  .form-switcher button:hover {
    transform: scale(1.1);
  }
  
  .form-switcher button.active {
    border-bottom: 2px solid #00ffcc;
  }
  
  .form-container {
    display: flex;
    flex-direction: column;
    align-items: center;
  }
  
  .form-group {
    margin-bottom: 10px;
    width: 100%;
    max-width: 300px;
  }
  
  label {
    display: block;
    margin-bottom: 10px;
    color: #00ffcc;
    font-family: 'Orbitron', sans-serif;
    letter-spacing: 0.5px;
  }
  
  .form-input {
    width: 100%;
    padding: 12px;
    background: transparent;
    border: 2px solid #00ffcc;
    border-radius: 8px;
    font-size: 16px;
    color: white;
    font-family: 'Orbitron', sans-serif;
    transition: border-color 0.3s ease, box-shadow 0.3s ease;
  }
  
  .form-input:focus {
    border-color: #00ffcc;
    box-shadow: 0 0 10px #00ffcc;
    outline: none;
  }
  
  .submit-button {
    background: linear-gradient(90deg, #00ffcc, #00d4ff);
    color: black;
    border: none;
    padding: 12px 24px;
    border-radius: 8px;
    cursor: pointer;
    font-size: 18px;
    font-family: 'Orbitron', sans-serif;
    text-transform: uppercase;
    transition: background 0.3s ease, transform 0.3s ease, box-shadow 0.3s ease;
  }
  
  .submit-button:hover {
    background: linear-gradient(90deg, #00d4ff, #00ffcc);
    transform: scale(1.05);
    box-shadow: 0 0 20px rgba(0, 212, 255, 0.9);
  }
  
  .submit-button:active {
    transform: scale(1.02);
    box-shadow: 0 5px 15px rgba(0, 0, 0, 0.3);
  }
  
  .cyber-slide-enter-active,
  .cyber-slide-leave-active {
    transition: all 0.5s ease-out;
    position: absolute;
    width: 100%;
  }
  
  .cyber-slide-enter-from {
    transform: translateX(-100%) skew(-10deg);
    opacity: 0;
    filter: hue-rotate(90deg) saturate(200%);
  }
  
  .cyber-slide-leave-to {
    transform: translateX(100%) skew(10deg);
    opacity: 0;
    filter: hue-rotate(-90deg) saturate(200%);
  }
  
  .cyber-slide-enter-active::before,
  .cyber-slide-leave-active::before {
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background: linear-gradient(45deg, transparent 20%, #00ffcc 20%, #00ffcc 40%, transparent 40%, transparent 60%, #00ffcc 60%, #00ffcc 80%, transparent 80%);
    background-size: 200% 200%;
    animation: glitch 0.5s linear infinite;
    opacity: 0.2;
    z-index: -1;
  }
  
  @keyframes glitch {
    0% {
      background-position: 0 0;
    }
    100% {
      background-position: 100% 100%;
    }
  }
  
  .form-input {
    border-color: #00ffcc;
    box-shadow: 0 0 10px rgba(0, 255, 204, 0.5);
  }
  
  .submit-button {
    background: linear-gradient(90deg, #00ffcc, #00d4ff);
    box-shadow: 0 0 15px rgba(0, 255, 204, 0.7);
  }
  
  .submit-button:hover {
    background: linear-gradient(90deg, #00d4ff, #00ffcc);
    box-shadow: 0 0 20px rgba(0, 212, 255, 0.9);
  }
  </style>