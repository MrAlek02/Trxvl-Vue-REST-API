<template>
  <section class="hero">
    <div class="hero-bg">
      <div class="container">
        <div class="title skeleton-text"></div>
        <div class="search-bar skeleton-box">
          <div class="search"></div>
          <div class="checks">
            <div class="check-cal"></div>
            <div class="check-cal"></div>
          </div>
          <div class="persons-icon"></div>
          <button class="skeleton-box"></button>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.skeleton-box {
  background: #ddd;
  border-radius: 8px;
  animation: pulse 1.5s infinite ease-in-out;
}

.skeleton-text {
  width: 80%;
  height: 100px;
  margin: 100px 0;
  border-radius: 8px;
  background: #ddd;
}

@keyframes pulse {
  0% {
    background-color: #e0e0e0;
  }
  50% {
    background-color: #f0f0f0;
  }
  100% {
    background-color: #e0e0e0;
  }
}
</style>
