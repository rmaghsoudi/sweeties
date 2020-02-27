<template>
  <div id="app">
    <h1>Sweeties</h1>
    <DessertList v-bind="{desserts, cart}" @add="addToCart"/>
  </div>
</template>

<script>
import DessertList from './components/DessertList.vue'

export default {
  name: 'App',
  components: {
    DessertList
  },
  data() {
    return {
      desserts : [{ id: 1, name: "cake", image: "./assets/logo.png"}, { id: 2, name: "cookie", image: "./assets/cookie-placeholder.jpg" }],
      cart: []
    }
  },
  methods: {
    addToCart(dessert) {
      this.cart.push({dessert})
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
