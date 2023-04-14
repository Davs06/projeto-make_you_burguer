<template>
  <div id="nav">
    <nav>
      <router-link to="/" id="logo-url"><img :src="logo" :alt="alt" id="logo"></router-link>
      <router-link to="/">Home</router-link> |
      <router-link to="/pedidos">Pedidos</router-link>
    </nav>
  </div>
</template>

<script>
export default {
    name: 'Navbar',
    props: ['logo', 'alt'],
}
</script>

<style scoped>

#nav{
    margin: 0;
    padding: 0;
}
nav{
    padding:15px 50px;
    background-color: #222;
    border-bottom: 4px solid #111;
    display: flex;
    justify-content: flex-end;
    align-items: center;

}

#logo-url {
    margin: auto;
    margin-left: 0;
}

nav a{
    text-decoration: none;
    font-size: 20px;
    margin: 5px;
    color: #fcba03;
    transition:.5s;
}

nav a:hover{
    color: #fff;
}

#logo{
    width: 50px;
    height: 50px;
}

</style>