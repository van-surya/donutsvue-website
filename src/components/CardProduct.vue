<template>
  <div class="card card-menu">
    <div class="card-body text-center">
      <img :src=" 'images/'+product.image" alt="" height="150px" width="150px"/>
      <h4>{{ product.name }}</h4>
      <p>IDR {{product.price}}</p>
      <button class="btn btn-add">
            <b-icon icon="plus" class="mr-2"></b-icon>Order
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: "CardProduct",
  props: ["product"],
};
</script> 