

<template>
  <div class="products-new">
    <h1>New Product</h1>
    <ul>
      <li v-for="error in errors">{{ error }}</li>
    </ul>
    <form v-on:submit.prevent="submit()">
      <div>
        Name: <input v-model="newProductName">
      </div>
      <div>
        Price: <input v-model="newProductPrice">
      </div>
      <div>
        Description: <input v-model="newProductDescription">
      </div>
      <div>
        Image URL: <input v-model="newProductImageURL">
      </div>
      <input type="submit" value="Create" class="btn btn-primary">
    </form>
  </div>
</template>

<style>
</style>

<script>
var axios = require('axios');

export default {
  data: function() {
    return {
      newProductName: "",
      newProductPrice: "",
      newProductDescription: "",
      newProductImageURL: "",
      errors: []
    };
  },
  created: function() {},
  methods: {
    createProduct: function() {
      console.log("Create the Product...");
      var params = {
                    name: this.newProductName,
                    price: this.newProductPrice,
                    description: this.newProductDescription,
                    image_url: this.newProductImageURL
                    };
      axios.post("/api/products", params)
        .then(response => {
          console.log("Success", response.data);
          this.$router.push("/");
        }).catch(error => {
          this.errors = error.response.data.errors;
        });
    }
  }
};
</script>