<template>
  <div>
    <b-navbar toggleable="lg" variant="faded" type="orange">
      <div class="container">
        <b-navbar-brand href="#">Donut's Vue</b-navbar-brand>

        <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

        <b-collapse id="nav-collapse" is-nav>
          <b-navbar-nav>
            <router-link class="nav-link" to="/">Home</router-link>
            <router-link class="nav-link" to="/menus">Menu</router-link>
            <!-- <b-nav-item href="#">Link</b-nav-item> -->
          </b-navbar-nav>

          <!-- Right aligned nav items -->
          <b-navbar-nav class="ml-auto">
            <b-navbar-nav>
              <router-link class="nav-link" to="/basket">
                <b-icon-bag class="mr-1"></b-icon-bag>
                <!-- IF update basket true show update basket else quality -->
                <span class="badge badge-chocolate my-auto">{{
                  updateBasket ? updateBasket.length : quality.length
                }}</span>
              </router-link>
            </b-navbar-nav>
          </b-navbar-nav>
        </b-collapse>
      </div>
    </b-navbar>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "NavbarComponent",
  data() {
    return {
      quality: [],
    };
  },
  props: ["updateBasket"],
  methods: {
    setQuality(data) {
      this.quality = data;
    },
  },
  mounted() {
    axios
      .get("http://localhost:3000/baskets")
      // handle success
      .then((response) => this.setQuality(response.data))
      .catch((error) => console.log(error));
  },
};
</script>
 