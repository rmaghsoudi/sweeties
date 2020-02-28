<template>
<div id="app">
  <div class="cart" >
    <div v-show="items.length > 0">
      <ul>
        <li v-for="(item, index) in items" :key="index" transition="fade">
          <p><strong>{{ item.quantity }}</strong> - {{ item.name }} <button @click="removeFromCart(item)">Remove</button></p>
        </li>
      </ul>
      <h3>Your total is {{ total }}</h3>
    </div>
    <div v-show="items.length === 0">
      <p>Your cart is empty!</p>
    </div>
  </div>
  </div>
</template>

<script>
// const items = [
//   {
//     name: "One-Punch Man, Vol. 5",
//     price: 10.02,
//     quantity: 1
//   },
//   {
//     name: "The Quintessential Quintuplets, Vol. 1",
//     price: 22.98,
//     quantity: 2
//   },
//   {
//     name: "Uzumaki: Spiral into Horror, Complete Deluxe Edition",
//     price: 25.19,
//     quantity: 1
//   },
//   {
//     name: "Tomie: Complete Edition",
//     price: 31.49,
//     quantity: 3
//   }
// ]
export default {
  name: 'Cart',
  props: ['items'],
  data: function() {
    return {
      // items: [],
      quantity: 1
    }
  },
  computed: {
    total: function() {
      let total = 0;
      for(let i = 0; i < this.items.length; i++) {
      
        total += (this.items[i].price * this.items[i].quantity);
      }
      return Math.round((total + Number.EPSILON) * 100) / 100;
    }
  },
  methods: {
    removeFromCart(item) {
      item.quantity -= 1;
      if(item.quantity < 1){
        this.items.splice(this.items.indexOf(item), 1);
      }
   
    }
  }
};

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
