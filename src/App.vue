<template>
  <Navbar :logo="logo_src" :alt="logo" />
  <router-view />
  <Footer />
</template>

<script>
import Navbar from "./components/Navbar.vue";
import Footer from "./components/Footer.vue";

export default {
  components: {
    Navbar,
    Footer,
  },
  data() {
    return {
      logo_src: "/img/logo.png",
      alt: "logo",
    };
  },
};
</script>


<style>
*{
  margin:0;
  padding: 0;
  box-sizing: border-box;
  font-family: helvetica;
}

</style>
