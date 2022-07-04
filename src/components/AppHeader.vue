<template>
  <header>
    <router-link :to="{ path: '/' }"><img alt="Vue logo" src="../assets/logo.png" height="50"></router-link>
    <p>Vue.js Application for PUNK API</p>
  </header>
</template>

<style lang="scss">
  header {
    display: flex;
    padding: .5rem 1rem;
    margin-bottom: 2rem;

    p {
      margin-left: 1rem;
    }
  }

  nav {
    margin-left: auto;

    ul {
      list-style: none;
    }

    ul li {
      display: inline-flex;
      margin-left: 1rem;
    }
  }
</style>
