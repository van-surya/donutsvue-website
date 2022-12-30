<template>
    <div class="container jumbotron mt-3">
        <div class="row">
        <div class="col-md-6 hero-lead order-1 ">
            <h1>TRY OUR BEST <span>DONUT'S</span> IN TOWN</h1>
            <p>
            Who loves donuts? Or Perhaps it would be easier to ask, "Who doesn't
            love donuts?" So, what are you waiting for, order our
            <span>fresh donuts</span>
            now!
            </p>
            <router-link to="/menus"  class="btn btn-custom">Order Now !</router-link>
        </div>
            <div class="col-md-6 hero-image order-md-2">
                <img src="../assets/images/hero.png" class="hero-img" alt="hero image"/>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "HeroComponent",
};
</script> 