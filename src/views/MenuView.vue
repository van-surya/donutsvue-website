<template>
  <div>
    <Navbar />
    <div class="container" style="margin-top: 4rem">
      <div class="head-menu">

        <h5 class="text-lead"><strong>List</strong> Menu</h5>

        <div class="input-group mb-3" style="width:200px;">
          <input v-model="search" @keyup="searchMenu"
            type="text"
            class="form-control"
            placeholder="Search" 
          /> 
        </div>

      </div>
      <div class="row mt-5 mb-5">
        <!-- Foreach in VueJS  -->
        <div
          class="col-md-3 mb-5"
          v-for="product in products"
          :key="product.id"
        >
          <!-- Insert to CardProduct  -->
          <CardProduct :product="product" />
        </div>
      </div>
    </div>
    <Footer />
  </div>
</template>


<script>
// @ is an alias to /src
import Navbar from "@/components/NavbarComponent.vue";
import CardProduct from "@/components/CardProduct.vue";
import Footer from "@/components/FooterComponent.vue";

import axios from "axios";

export default {
  name: "MenuView",
  components: {
    Navbar,
    CardProduct,
    Footer,
  },
  data() {
    return {
      products: [],
      search: '',
    };
  },
  methods: {
    setProducts(data) {
      this.products = data;
    },
    searchMenu(){
      axios
      .get("http://localhost:3000/products?q="+this.search)
      // handle success
      .then((response) => this.setProducts(response.data))
      .catch((error) => console.log(error));
    }
  },
  mounted() {
    axios
      .get("http://localhost:3000/products")
      // handle success
      .then((response) => this.setProducts(response.data))
      .catch((error) => console.log(error));
  },
};
</script>
