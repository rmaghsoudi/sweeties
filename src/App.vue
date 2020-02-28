<template>
  <div id="app">
    <h1>Sweeties</h1>
    <DessertList v-bind="{ desserts }" @add="addToCart" />
    <Cart v-bind="{items}"/>
  </div>
</template>

<script>
import DessertList from "./components/DessertList.vue";
import Cart from "./components/Cart.vue";

export default {
  name: "App",
  components: {
    DessertList,
    Cart
  },
  data() {
    return {
      desserts: [
        {
          id: 1,
          inventory: 3,
          name: "cake",
          image: "https://static.turbosquid.com/Preview/2014/07/08__14_45_55/chocolatecake1.jpg7e1f6d88-de30-4357-bd02-a3c74e5b5b90Zoom.jpg",
          description: "Cake is great!",
          price: 18.25,
          quantity: 0
        },
        {
          id: 2,
          inventory: 5,
          name: "cookie",
          image: "https://images.onerichs.com/CIP/preview/thumbnail/uscm/9840",
          description: "Cookies are great!",
          price: 2.25,
          quantity: 0
        }
      ],

      items: [
        { id: 3,
          inventory: 11,
          name: "One-Punch Man, Vol. 5",
          image: "logo.png",
          price: 10.02,
          quantity: 1
        },
        { id: 4,
          inventory: 7,
          name: "The Quintessential Quintuplets, Vol. 1",
          image: "logo.png",
          price: 22.98,
          quantity: 2
        },
        { id: 5,
          inventory: 3,
          name: "Uzumaki: Spiral into Horror, Complete Deluxe Edition",
          image: "logo.png",
          price: 25.19,
          quantity: 1
        },
        { id: 6,
          inventory: 9,
          name: "Tomie: Complete Edition",
          image: "logo.png",
          price: 31.49,
          quantity: 3
        }
      ]
    };
  },
  methods: {

    addToCart(dessert) {
      const items = this.items;
      const desserts = this.desserts;
       dessert.inventory -= 1;
      if(dessert.inventory < 1){
        desserts.splice(desserts.indexOf(dessert), 1);
      }
      if(items.includes(dessert)){
        for (let i = 0; i < items.length; i++) {
            if(items[i].id === dessert.id) {
                items[i].quantity += 1
            }  
        }
      }
      else{
        dessert.quantity += 1
         this.items.push(dessert);
      }
      console.log(this.desserts)

    }
  }
};
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
