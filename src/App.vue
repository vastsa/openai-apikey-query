<script setup lang="ts">
import HelloWorld from './components/HelloWorld.vue'
import TheWelcome from './components/TheWelcome.vue'
</script>

<template>
  <header>
    <img alt="Vue logo" class="logo" src="./assets/logo.png" width="125" height="125" />

    <div class="wrapper">
      <HelloWorld msg="Usage Query" />
    </div>
  </header>

  <main>
    <TheWelcome />
  </main>

  <main style="text-align: center">
    <a class="a" href="https://ailink.pw/" target="_blank">AiLink</a>
    <a class="a" href="https://github.com/vastsa" target="_blank">Github</a>
  </main>
</template>

<style scoped>
header {
  line-height: 1.5;
}
.a{
  margin-left: 1rem;
}
.logo {
  display: block;
  margin: 0 auto 2rem;
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
}
</style>
