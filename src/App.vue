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
.main-container{
  margin: 50px;
  min-height: 250px;
}

h1{
  text-align: center;
  font-size: 40px;
  margin-bottom: 30px;
  color: #222;
}

</style>
