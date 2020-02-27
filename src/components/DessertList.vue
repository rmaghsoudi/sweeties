<template>
<div class="dessert-list" >
    <div>
      <Dessert @add="addToCart" v-bind:key="dessert.id" v-for="dessert in desserts" class="dessert-item" v-bind="{dessert, cart}"/>
    </div>
</div>
</template>

<script>
import Dessert from './Dessert.vue'

export default {
  name: "DessertList",
  components: { Dessert 
  },
  props: ["desserts", "cart"],
   methods: {
    addToCart(dessert){
    this.$emit('add', dessert)
    }
 
  }

};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

.dessert-list {
 display: flex;
 flex-direction: row;
 justify-content: center;
 flex-wrap: wrap;
} 
</style>
