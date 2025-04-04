<script setup>
import CityTime from './components/CityTime.vue'
import Intro from './components/Intro.vue'
// import TheWelcome from './components/TheWelcome.vue'
</script>

<template>
  <header>
    
    <img alt="Vue logo" class="logo" src="./assets/aoyuki.png" width="250" height="400" />
    <div class="wrapper">
      Welcome to <span class="v-style">City Time Viewer</span> a Vue-based web application that allows users to check the current time across various cities worldwide. Designed with a sleek and modern UI, the project aims to provide a seamless experience for global time tracking.
      <br>
      <br>
      <Intro />
    </div>
   
  </header>


  <main>
    <CityTime />
  </main>
</template>

<style scoped>
header {
  line-height: 1.5;
}

.v-style {
  color: #08889f;
  font-size: 22px;
  font-weight: bold;
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
    color:rgb(0, 255, 255);
  }
}
</style>
