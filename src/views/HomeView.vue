<script>
export default {
  data: function () {
    return {
      message: "Welcome to Vue.js!",
      text: "Hey this is working",
      showInfo: false,
      image: "https://imageio.forbes.com/blogs-images/mitchwallace/files/2018/02/mightymax-1200x1045.jpg?format=jpg&width=960"
    };
  },
  created: function () {},
  methods: {
    toggleTheThing: function () {
      console.log("it's happening");
      this.showInfo = !this.showInfo
    },
  },
};
</script>

<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <h2>{{ text }}</h2>
    <p>This is just plain text</p>
    <button v-on:click="toggleTheThing">Thing toggle</button>
    {{ showInfo }}
    <div v-if="showInfo">
    THIS IS THE THING
  </div>
    <img v-bind:src="image" />
  </div>
</template>

<style></style>
