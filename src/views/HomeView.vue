<template>
  <div class="home">
    <Navbar />
    <Hero />
    <div class="container">
      <div class="best-donuts">
        <h2>Best <strong>Donut's</strong></h2>
        <router-link to="/menus" class="show-all">Show All</router-link>
        <div class="row mt-5 mb-5" >
        <!-- Foreach in VueJS  -->
          <div class="col-md-3" v-for="product in products" :key="product.id">
          <!-- Insert to CardProduct  -->
            <CardProduct :product="product"/>
          </div>
        </div>
      </div>
    </div>
    <Footer/>
  </div>
</template>

<script>
// @ is an alias to /src
import Navbar from "@/components/NavbarComponent.vue";
import Hero from "@/components/HeroComponent.vue";
import CardProduct from "@/components/CardProduct.vue";
import Footer from "@/components/FooterComponent.vue";

import axios from "axios";

export default {
  name: "HomeView",
  components: {
    Navbar,
    Hero,
    CardProduct,
    Footer,
  },
  data() {
    return {
      products: [],
    };
  },
  methods: {
    setProducts(data) {
      this.products = data;
    },
  },
  mounted() {
    axios
      .get("http://localhost:3000/best-products")
        // handle success
      .then((response) => this.setProducts(response.data))
      .catch((error) => console.log(error))
  },
};
</script>
