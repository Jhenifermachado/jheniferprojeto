<script setup>
import HeaderComp from "@/components/Template/HeaderComp.vue";
import FooterComp from "@/components/Template/FooterComp.vue";
</script>

<template>
  <HeaderComp />
  <main>
    <RouterView />
  </main>
  <FooterComp />
</template>

<style>
@import "@/assets/base.css";

#app {
  max-width: 1280px;
  margin: 0 auto;
  height: 100vh;
  /* padding: 2rem; */

  font-weight: normal;
}
a {
  color: inherit;
  text-decoration: none;
}

footer {
  height: 10%;
  background-color: #db7093;
  color: black;
  font-size: 1.3rem;
  display: flex;
  align-items: center;
  padding-left: 20px;
}
header span {
  padding-left: 20px;
  padding-right: 20px;
}
main {
  height: 80%;
}
</style>
