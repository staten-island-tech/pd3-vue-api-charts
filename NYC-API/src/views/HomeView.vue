<script setup>
import { RouterLink, RouterView } from "vue-router";
</script>

<template>
  <main>
    <h1 data-aos="zoom-in-down" data-aos-duration="3000">
      NYC dog license data charts here:
    </h1>
    <header>
      <nav data-aos="zoom-in-up" data-aos-duration="3000">
        <RouterLink to="/">Home:</RouterLink>
        <RouterLink to="/about">About:</RouterLink>
        <RouterLink to="/bar">Bar Chart:</RouterLink>
        <RouterLink to="/pie">Pie Chart:</RouterLink>
      </nav>
    </header>
  </main>
</template>

<style>
h1 {
  font-size: 40px;
  text-align: center;
  margin: 40px 0px;
}
header {
  line-height: 1.5;
  max-height: 100vh;
}

nav {
  width: 100%;
  font-size: 30px;
  text-align: center;
  margin-top: 1rem;
}

nav a.router-link-exact-active {
  color: var(--color-text);
}

nav a.router-link-exact-active:hover {
  background-color: transparent;
}

nav a {
  display: inline-block;
  padding: 0 1rem;
  border-left: 1px solid var(--color-border);
}

nav a:first-of-type {
  border: 0;
}
</style>
