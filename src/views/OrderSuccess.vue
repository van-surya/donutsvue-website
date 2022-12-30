<template>
  <div>
    <Navbar />
    <div class="container" style="margin-top: 4rem">
      <div class="card border-0">
        <div class="card-body text-center">
          <img
            src="../assets/images/success.png" 
            alt="success.png" class="succes-img"
          />

          <h5 style="color:chocolate;" class="text-lead"><strong>SUCCESS</strong></h5>
          <p style="color:chocolate;">
            We are processing your order <br /><strong style="color:#6b443d">thank you,</strong>
            please wait
          </p>
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

export default {
  name: "OrderSuccess",
  components: {
    Navbar,
    Footer,
  },
};
</script>
