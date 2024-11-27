<script setup>
import Header from '../components/Header.vue';
import Footer from '../components/Footer.vue';
</script>

<template>
  <Header/>
  <div class="hero">
    <div class="overlay">
      <div class="form-container">
        <h2>Create an Account</h2>
        <form>
          <input type="text" placeholder="First Name" class="input-field" required>
          <input type="text" placeholder="Last Name" class="input-field" required>
          <input type="email" placeholder="Email" class="input-field" required>
          <input type="password" placeholder="Password" class="input-field" required>
          <input type="password" placeholder="Re-enter Password" class="input-field" required>
          <button type="submit" class="button register">Register</button>
        </form>
      </div>
    </div>
  </div>
  <Footer/>
</template>

<style scoped>
.hero {
  background-image: linear-gradient(rgba(0, 0, 0, 0.5), rgba(0, 0, 0, 0.5)), url(../assets/hero.jpg);
  height: 90vh;
  background-size: cover;
  background-attachment: fixed;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
  position: relative;
  color: white;
}

.overlay {
  position: absolute;
  inset: 0;
  background: rgba(0, 0, 0, 0.6);
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  padding: 0 20px;
}

.navbar {
  background-color: transparent;
  width: 100%;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 20px;
  position: absolute;
  top: 0;
}

.navbar h1 {
  font-family: 'Montserrat', sans-serif;
  color: #FFD700;
  margin-left: 20px;
}

.navbar .login {
  background-color: transparent;
  color: white;
  border: 2px solid #E6B800;
  padding: 10px 20px;
  font-size: 16px;
  font-weight: bold;
  transition: 0.3s;
  border-radius: 30px;
}

.navbar .login:hover {
  background: #E6B800;
  color: black;
  transform: scale(1.2);
}

.form-container {
  background: rgba(28, 20, 20, 0.8);
  padding: 40px;
  border-radius: 20px;
  box-shadow: 0px 4px 10px rgba(0, 0, 0, 0.7);
  text-align: center;
  width: 90%;
  max-width: 400px;
  color: white;
}

.form-container h2 {
  font-family: 'Oswald', sans-serif;
  color: #FFD700;
  margin-bottom: 20px;
}

.input-field {
  width: 100%;
  padding: 10px 15px;
  margin: 10px 0;
  border: 2px solid #E6B800;
  border-radius: 8px;
  background: transparent;
  color: white;
  font-size: 16px;
}

.input-field::placeholder {
  color: #B0B0B0;
}

.input-field:focus {
  outline: none;
  border-color: #FFD700;
}

.button.register {
  background-color: #E6B800;
  color: black;
  border: none;
  padding: 10px 20px;
  font-size: 16px;
  font-weight: bold;
  border-radius: 20px;
  transition: 0.3s;
  cursor: pointer;
  width: 100%;
}

.button.register:hover {
  background-color: #FFD700;
  color: black;
  transform: scale(1.1);
}
</style>
