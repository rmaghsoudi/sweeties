<template>
  <div id="app">
<<<<<<< HEAD
    <h1>Sweeties</h1>
    <DessertList v-bind="{desserts, cart}" @add="addToCart"/>
=======
    <img alt="Vue logo" src="./assets/logo.png">
    <Cart />
>>>>>>> 1db9bf9d0875641ea439196612ce48b295f85339
  </div>
</template>

<script>
<<<<<<< HEAD
import DessertList from './components/DessertList.vue'
=======
import Cart from './components/Cart.vue'
>>>>>>> 1db9bf9d0875641ea439196612ce48b295f85339

export default {
  name: 'App',
  components: {
<<<<<<< HEAD
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
      console.log(this.cart[0])
    }
=======
    Cart
>>>>>>> 1db9bf9d0875641ea439196612ce48b295f85339
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
