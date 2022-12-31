<template>
  <div>
    <Navbar :updateBasket="baskets" />

    <nav aria-label="breadcrumb">
      <ol class="breadcrumb container">
        <li class="breadcrumb-item">
          <router-link to="/">Home</router-link>
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
      <div
        class="card mt-3"
        style="border: 1px solid pink !important; padding: 1rem 1rem !important"
      >
        <div class="card-body">
          <div class="table-responsive">
            <table class="table align-middle table-borderless">
              <thead>
                <tr>
                  <th class="text-center">No</th>
                  <th style="width:150px; !important">Image</th>
                  <th style="width:200px; !important">Name</th>
                  <th style="width:300px; !important">Note</th>
                  <th style="width:100px; !important" class="text-center">
                    Quality
                  </th>
                  <th style="width:250px; !important" class="text-center">
                    Price
                  </th>
                  <th style="width:300px; !important" class="text-center">
                    Total
                  </th>
                  <th style="width:200px; !important" class="text-center">
                    Action
                  </th>
                </tr>
              </thead>
              <tbody>
                <!-- Foreach in hire -->
                <tr v-for="(basket, index) in baskets" :key="basket.id">
                  <th>{{ index + 1 }}</th>
                  <td>
                    <img
                      :src="'../images/' + basket.products.image"
                      :alt="basket.products.image"
                      class="img-basket"
                    />
                  </td>
                  <td>{{ basket.products.name }}</td>
                  <td>{{ basket.note ? basket.note : "-" }}</td>
                  <td class="text-center">{{ basket.quality }}</td>
                  <td class="text-center">IDR {{ basket.products.price }}</td>
                  <td class="text-center">
                    <strong>
                      IDR {{ basket.products.price * basket.quality }}</strong
                    >
                  </td>
                  <td class="text-center">
                    <button
                      class="btn btn-outline-danger"
                      @click="deleteBasket(basket.id)"
                    >
                      <b-icon icon="trash"></b-icon>
                    </button>
                  </td>
                </tr>
                <tr>
                  <td colspan="7" align="right" class="text-start">
                    <strong>Total Amount : </strong>
                  </td>
                  <td>
                    <strong>IDR {{ totalAmount }}</strong>
                  </td>
                </tr>
              </tbody>
            </table>
          </div>
          <div class="row justify-content-end">
            <div class="col-md-6">
              <form v-on:submit.prevent>
                <div class="mb-3">
                  <label class="form-label">Name</label>
                  <input
                    type="text"
                    class="form-control"
                    v-model="order.name"
                    placeholder="Your Name"
                  />
                </div>
                <div class="mb-3">
                  <label class="form-label">Phone</label>
                  <input
                    type="number"
                    class="form-control"
                    v-model="order.phone"
                    placeholder="08xxxxxxxx"
                  />
                </div>

                <div class="text-center">
                  <button
                    type="submit"
                    class="btn btn-submit"
                    @click="Checkout"
                  >
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
  name: "BasketsView",
  components: {
    Navbar,
    Footer,
  },
  data() {
    return {
      baskets: [],
      order: {},
    };
  },
  methods: {
    setBaskets(data) {
      this.baskets = data;
    },
    deleteBasket(id) {
      axios
        .delete("http://localhost:3000/baskets/" + id)
        // handle success
        .then(() => {
          this.$toast.success("Data deleted successfully.", {
            type: "success",
            position: "top",
            duration: 2000,
            dismissible: true,
          });

          //update data
          axios
            .get("http://localhost:3000/baskets")
            // handle success
            .then((response) => this.setBaskets(response.data))
            .catch((error) => console.log(error));
        })
        .catch((err) => console.log(err));
    },
    Checkout() {
      // if input name and phone true
      if (this.order.name && this.order.phone) {
        this.order.baskets = this.baskets;
        axios
          .post("http://localhost:3000/orders", this.order)
          // handle success
          .then(() => {
            //delete items on basket
            this.baskets.map(function (item) {
              return axios
                .delete("http://localhost:3000/baskets/" + item.id)
                .catch((error) => console.log(error));
            });
            this.$router.push({ path: "/my-order" });

            this.$toast.success("Successfully Order", {
              type: "success",
              position: "top",
              duration: 2000,
              dismissible: true,
            });
          })
          .catch((err) => console.log(err));
      } else {
        this.$toast.error("Sorry you did not enter a name or phone number", {
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
      .get("http://localhost:3000/baskets")
      // handle success
      .then((response) => this.setBaskets(response.data))
      .catch((error) => console.log(error));
  },
  // for total
  computed: {
    totalAmount() {
      return this.baskets.reduce(function (items, data) {
        return items + data.products.price * data.quality;
      }, 0);
    },
  },
};
</script>
