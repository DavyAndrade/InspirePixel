<script setup></script>

<template>
  <header class="navbar">
    <h2 class="navbar__logo">InspirePixel</h2>
    <nav></nav>
  </header>
</template>

<style scoped lang="scss">
.navbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1rem;
  background-color: #fff;
  position: sticky;
  top: 0;
  left: 0;
  z-index: 100;
  width: 100%;

  &__logo {
    font-size: 1.5rem;
    font-weight: bold;
    cursor: pointer;
    color: #333;
  }
}
</style>
