<template>
  <div class="card card-menu">
    <div class="card-body text-center">
      <img :src=" 'images/'+product.image" :alt="product.image" height="150px" width="150px"/>
      <h4>{{ product.name }}</h4>
      <p>IDR {{product.price}}</p>
      <router-link :to="'/menus/'+product.id" class="btn btn-add">
            <b-icon icon="plus" class="mr-2"></b-icon>Order
      </router-link>
    </div>
  </div>
</template>

<script>
export default {
  name: "CardProduct",
  props: ["product"],
};
</script> 