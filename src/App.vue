<script setup>
import { ref, computed } from "vue";
import Home from "./App.original.vue";
import Sandbox from "./Sandbox.vue";

const routes = {
  "/": Home,
  "/sandbox": Sandbox,
};

const currentPath = ref(window.location.hash);

window.addEventListener("hashchange", () => {
  currentPath.value = window.location.hash;
});

const currentView = computed(() => {
  return routes[currentPath.value.slice(1) || "/"] || NotFound;
});
</script>

<template>
  <header>
    <div>
      <a href="#/">Home</a> | <a href="#/sandbox">Sandbox</a> |
      <a href="#/non-existent-path">Broken Link</a>
    </div>
  </header>
  <main>
    <component :is="currentView" />
  </main>
</template>

<style scoped>
header {
  height: 3rem;
  display: flex;
  flex-direction: row;
}

header div {
    padding: 1rem;
}

header div a {
    padding: .5rem;
}

main {
  max-width: 900px;
  margin: 0 auto;
  padding: 2rem;
}
</style>
