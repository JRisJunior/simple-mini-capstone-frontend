<script>
import axios from 'axios';
export default {
  data: function () {
    return {
      message: "Welcome to Vue.js!",
      text: "Hey this is working",
      showInfo: false,
      products: [],
      newProductParams: {},
      currentProduct: {},
    };
  },
  created: function () {
    console.log("page loading");
    this.indexProducts();
  },
  methods: {
    indexProducts: function () {
      axios.get("http://localhost:3000/products.json").then((response) => {
        console.log("products index", response)
        this.products = response.data;
      });
    },
    createProduct: function () {
      axios.post("http://localhost:3000/products/", this.newProductParams).then((response) => {
        console.log("product create", response);
        this.products.push(response.data);
        this.newProductParams = {};
      })},
    showProduct: function (product) {
      this.currentProduct = product;
      document.querySelector("#product-details").showModal();
    }
    },
  };
</script>

<template>
  <div class="home">
    <h1>New Product</h1>
    <div>
      <p>Name: <input type="text" v-model="newProductParams.name" /></p>
      <p>price: <input type="text" v-model="newProductParams.price" /></p>
      <p>description: <input type="text" v-model="newProductParams.description" /></p>
      <p> supplier id: <input type="text" v-model="newProductParams.supplier_id" /></p>
      <button v-on:click="createProduct()">Create Product</button>
    </div>
    <h1>{{ message }}</h1>
    <h2>{{ text }}</h2>
    <div v-for="product in products" v-bind:key="product.id">
    <h3>{{ product.name }}</h3>
    <p>{{ product.price }}</p>
    <button v-on:click="showProduct(product)">More product info</button>
    <hr />
  </div>
  <dialog id="product-details">
  <form method="dialog">
    <h1>Product info</h1>
    <p>Name: {{ currentProduct.name }}</p>
    <p>Price: {{ currentProduct.price }}</p>
    <p>Description: {{ currentProduct.description }}</p>
    <!-- <p>Supplier: {{ currentProduct.supplier['name'] }}</p> -->
    <button>Close</button>
  </form>
</dialog>
  </div>
</template>

<style></style>
