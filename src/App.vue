<script setup>
import { ref } from "vue"
import { RouterLink, RouterView } from 'vue-router'
import HelloWorld from './components/HelloWorld.vue'
const userId = ref();
const setUser = () => {
  if (!userId.value) return null;
  window._ce.setUserId(userId.value);
}
const clearUserId = () => {
  window._ce.clearUserId();
}
</script>

<template>
  <header>
    <img alt="Vue logo" class="logo" src="@/assets/logo.svg" width="125" height="125" />

    <div class="wrapper">
      <HelloWorld msg="You did it!" />
      <div class="flex justify-center items-center w-full my-2 py-2">
        <input v-model="userId" placeholder="Set user id" type="text" class="p-4 border-2 border-green-600 rounded-xl">
        <button @click="setUser"
          class="p-4 bg-green-600 rounded-xl mx-2 font-medium text-white hover:bg-green-500">Set</button>
        <button @click="clearUserId" class="p-4 bg-gray-600 rounded-xl mx-2 font-medium text-white hover:bg-gray-500">Clear User</button>
      </div>

      <nav>
        <RouterLink to="/">Home</RouterLink>
        <RouterLink to="/about">About</RouterLink>
      </nav>
    </div>
  </header>

  <RouterView />
</template>

<style scoped>
header {
  line-height: 1.5;
  max-height: 100vh;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

nav {
  width: 100%;
  font-size: 12px;
  text-align: center;
  margin-top: 2rem;
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
    margin-left: -1rem;
    font-size: 1rem;

    padding: 1rem 0;
    margin-top: 1rem;
  }
}
</style>
