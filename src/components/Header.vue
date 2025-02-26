<template>
  <header class="header">
    <router-link to="/" class="logo">trxvl.</router-link>
    <nav class="navbar">
      <router-link to="/">Home</router-link>
      <a href="#">Stays</a>
      <a href="#">Flights</a>
      <a href="#">Packages</a>
      <a href="#">Sign Up</a>
    </nav>
  </header>
</template>

<style scoped>
.header {
  position: fixed;
  width: 100%;
  padding: 1.3rem 10%;
  display: flex;
  justify-content: space-between;
  align-items: center;
  background-color: transparent;
  z-index: 100;
  box-shadow: 0 8px 16px rgba(0, 0, 0, 0.2);
}

.logo {
  font-size: 36px;
  color: white;
  text-decoration: none;
  font-weight: 700;
  background-color: transparent;
}

.logo:hover {
  opacity: 0.8;
}

.navbar {
  background-color: transparent;
  padding-right: 250px;
}

.navbar a {
  font-size: 18px;
  color: white;
  text-decoration: none;
  font-weight: 400;
  margin-right: 40px;
}

.navbar a:hover {
  opacity: 0.8;
}

.navbar a.active {
  border-bottom: 1px solid white;
}

@media (max-width: 1000px) {
  .header {
    justify-content: center;
    margin: 0;
    padding: 0;
    margin-top: 20px;
    padding-bottom: 20px;
  }
  .logo {
    font-size: 24px;
  }
  nav {
    display: none;
  }
}
</style>
