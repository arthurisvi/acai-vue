<template>
  <div id="nav">
    <router-link to="/" id = "logo-url">
        <img :src="logo" :alt="alt" id= "logo">
    </router-link>
    <router-link to="/">Home</router-link> |
    <router-link to="/pedidos">Pedidos</router-link>
  </div>
</template>

<script>
export default{
    name: 'Navbar',
    props: ["logo", "alt"]
}

</script>

<style scoped>

    #nav{
        background-color: rgb(132, 181, 28, 1);
        border-bottom: 4px solid #4C2D51;
        padding: 15px 50px;
        display: flex;
        justify-content: flex-end;
        align-items: center;
    }   

    #nav a{
        text-decoration: none;
        color: #FFF;
        margin: 12px;
        transition: 0.5s
    }

    #nav a:hover{
        color: #4C2D51
    }

    #nav #logo-url{
        margin: auto;
        margin-left: 0;
    }

    #logo{
        width: 60px;
        height: 60px;
    }

</style>