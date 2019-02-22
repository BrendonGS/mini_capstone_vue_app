<template>
  <div class="products-edit">
    <img :src="prodi">
    <h1>{{ product.name }}</h1>
    <h1>{{ product.description }}</h1>
    <h1>{{ message.price }}</h1>
    <h1>{{ message }}</h1>
  </div>
</template>

<style>
</style>

<script>
var axios = require('axios');
export default {
  data: function() {
    return {
      product: {
        id: "", 
        name: "", 
        description: "", 
        image_url: "", 
        price: "", 
        tax: "", 
        total: "", 
        formatted: {
          price: "", 
          tax: "", 
          total: ""}
      }
    };
  },
  created: function() {
    axios.get("/api/products/" + this.$route.params.id)
    .then(response => {
      console.log(response.data);
      this.product = response.data;
    });
  },
  methods: {}
};
</script>