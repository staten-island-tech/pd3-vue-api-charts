<script setup>
import { RouterLink, RouterView } from "vue-router";
</script>

<template>
  <div class="app">
    <header>
      <nav>
        <router-link to="/" class="hello">
          <div class="image">
            <img
              class="image"
              src="https://3.files.edl.io/aeb1/20/12/02/154937-46cc468f-b7f4-4bb3-945e-3265bdb605d4.jpg"
              alt="home"
            />
          </div>
        </router-link>
        <RouterLink to="/about">About:</RouterLink>
        <RouterLink to="/bar">Bar Chart:</RouterLink>
        <RouterLink to="/pie">Pie Chart:</RouterLink>
      </nav>
    </header>
    <RouterView class="routerview"></RouterView>
  </div>
</template>

<style scoped>
header {
  line-height: 1.5;
  max-height: 100vh;
}

nav {
  width: 100%;
  font-size: 20px;
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

.app {
  height: 100vh;
  width: 100vw;
}

.image {
  height: 3vw;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }

  nav {
    text-align: left;
    margin-left: 0rem;
    font-size: 1rem;

    padding: 0rem 0;
    margin-top: 1rem;
  }
}
</style>
