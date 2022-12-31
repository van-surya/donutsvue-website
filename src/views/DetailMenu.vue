<template>
  <div>
    <Navbar />

    <nav aria-label="breadcrumb">
      <ol class="breadcrumb container">
        <li class="breadcrumb-item">
          <router-link to="/">Home</router-link>
        </li>
        <li class="breadcrumb-item">
          <router-link to="/menus">Menu</router-link>
        </li>
        <li class="breadcrumb-item active" aria-current="page">Detail</li>
      </ol>
    </nav>

    <div class="container">
      <div class="head-menu">
        <h5 class="text-lead">
          <strong>Detail </strong>
        </h5>
      </div>
      <div class="card-detail">
        <div class="row">
          <div class="col-md-6">
            <img
              :src="'../images/' + product.image"
              :alt="product.image"
              class="detail-img"
            />
          </div>
          <div class="col-md-6">
            <h2>{{ product.name }}</h2>
            <p>Code : {{ product.code_product }}</p>
            <h4>IDR {{ product.price }}</h4>
            <p>
              Lorem ipsum dolor sit amet consectetur adipisicing elit. Neque
              deleniti ut a rerum aspernatur nihil, delectus, hic eius
              voluptatibus ducimus non
            </p>
            <form v-on:submit.prevent>
              <div class="mb-3 row">
                <label class="col-sm-2 col-form-label">Quality</label>
                <div class="col-sm-10">
                  <input
                    style="width: 120px"
                    type="number"
                    
                    class="form-control"
                    v-model="order.quality"
                  />
                </div>
              </div>
              <div class="mb-3 row">
                <label class="col-sm-2 col-form-label">Note</label>
                <div class="col-sm-10">
                  <textarea
                    class="form-control"
                    rows="3"
                    v-model="order.note"
                    placeholder="Enter your request order"
                  ></textarea>
                </div>
              </div>
              <div class="text-center">
                <button type="submit" class="btn btn-submit" @click="orderMenu">
                  Submit
                  <b-icon
                    class="my-auto"
                    style="margin-left: 1rem"
                    icon="cart-plus-fill"
                  ></b-icon>
                </button>
              </div>
            </form>
          </div>
        </div>
      </div>
    </div>
    <Footer />
  </div>
</template>


<script>
// @ is an alias to /src
import Navbar from "@/components/NavbarComponent.vue";
import Footer from "@/components/FooterComponent.vue";

import axios from "axios";

export default {
  name: "DetailMenu",
  components: {
    Navbar,
    Footer,
  },

  data() {
    return {
      product: {},
      order: {},
    };
  },

  methods: {
    setProduct(data) {
      this.product = data;
    },
    orderMenu() {
      //  Validation
      if (this.order.quality) {
        this.$router.push({path: '/basket'})
        this.order.products = this.product;
        axios
          .post("http://localhost:3000/baskets", this.order)
          .then(() => {
            this.$toast.success("Successfully added.", {
              type: "success",
              position: "top",
              duration: 2000,
              dismissible: true,
            });
          })
          .catch((err) => console.log(err));
      } else {
        this.$toast.error("Quality must be filled !", {
          type: "error",
          position: "top",
          duration: 2000,
          dismissible: true,
        });
      }
    },
  },
  mounted() {
    axios
      .get("http://localhost:3000/products/" + this.$route.params.id)
      // handle success
      .then((response) => this.setProduct(response.data))
      .catch((error) => console.log(error));
  },
};
</script>
