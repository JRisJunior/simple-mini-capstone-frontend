<script>
import axios from 'axios';
export default {
  data: function () {
    return {
      message: "Welcome to Vue.js!",
      text: "Hey this is working",
      showInfo: false,
      image: "https://imageio.forbes.com/blogs-images/mitchwallace/files/2018/02/mightymax-1200x1045.jpg?format=jpg&width=960",
      products: [],
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
    },
  };
</script>

<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <h2>{{ text }}</h2>
    <div v-for="product in products" v-bind:key="product.id">
    <h3>{{ product.name }}</h3>
    <p>{{ product.price }}</p>
    <hr />
  </div>
  </div>
</template>

<style></style>
