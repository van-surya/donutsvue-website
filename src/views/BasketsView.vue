<template>
  <div>
    <Navbar />

    <nav aria-label="breadcrumb">
      <ol class="breadcrumb container">
        <li class="breadcrumb-item">
          <router-link to="/home">Home</router-link>
        </li>
        <li class="breadcrumb-item">
          <router-link to="/menus">Menu</router-link>
        </li>
        <li class="breadcrumb-item active" aria-current="page">Basket</li>
      </ol>
    </nav>

    <div class="container">
      <div class="head-menu">
        <h5 class="text-lead">
          <strong>Basket</strong>
        </h5>
      </div>
       
    </div>
    <Footer />
  </div>
</template>


<script>
// @ is an alias to /src
import Navbar from "@/components/NavbarComponent.vue";
import Footer from "@/components/FooterComponent.vue";

export default {
  name: "BasketsView",
  components: {
    Navbar,
    Footer,
  }, 
};
</script>
