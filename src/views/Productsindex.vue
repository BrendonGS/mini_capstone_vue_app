
<template>
  <div class="recipes-index">
    <h1>All Products</h1>
    <div v-for="product in products">
      <h2>{{ product.name }}</h2> 
      <img v-bind:src="product.image_url" v-bind:alt="product.name">
      <div>
        <button v-on:click="showProduct(product)">More Info</button>
      </div>
      <div v-if="product === currentProduct">
      <p>{{ product.formatted.price }}</p>
      <p>{{ product.description }}</p>
      <p>{{ product.image_url }}</p>

      <div>
        <h4>Edit Product</h4>
      </div>
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
          <button v-on:click="updateProduct(product)">Update</button>
          <button v-on:click="destroyProduct(product)">Delete</button>
        </div>
      </div>
    </div>
  </div>
</template>

<style>
img{
  width: 250px;
}
</style>

<script>
var axios = require('axios');

export default {
  data: function() {
    return {
      products: [],
      createProduct: {}
    };
  },
  created: function() {
    axios.get("/api/products")
      .then(response => {
        this.products = response.data;
      });
  },
  methods: {
    showProduct: function(inputProduct) {
      if (this.currentProduct === inputProduct) {
        this.currentProduct = {};
      } else {
        this.currentProduct = inputProduct;
      }
    },
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
          this.products.push(response.data);
        });
    },
    updateProduct: function(inputProduct) {
      var params = {
        name: inputProduct.name,
        price: inputProduct.price,
        description: inputProduct.description,
        image_url: inputProduct.image_url
      };


      axis.patch("/api/products" + inputProduct.id, params)
      .then(response => {
        console.log("success", response.data);
        inputProduct = response.data;
      });
    }
  }
};
</script>
