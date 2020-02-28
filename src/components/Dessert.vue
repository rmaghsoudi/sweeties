<template>
  <!-- <div class="dessert-item"> -->
  <md-card>
    <md-ripple>
      <md-card-header>
      
        <md-card-header-text>
          <div class="md-title">{{ dessert.name }}</div>
            <div class="md-subhead">{{stock}}</div>
        </md-card-header-text>
     
          <md-card-media>
           <img v-bind:src="dessert.image" alt="Dessert">
        </md-card-media>
      </md-card-header>
      <md-content>
        ${{ dessert.price }}
      </md-content>
      <md-card-expand>
        <md-card-actions>
          <div>
            <md-button v-on:click="addCart(dessert)">Add to Cart</md-button>
            <md-button>
              <md-icon>favorite</md-icon>
            </md-button>
          </div>
          <md-card-expand-trigger>
            <md-button class="md-icon-button">
              <md-icon>keyboard_arrow_down</md-icon>
            </md-button>
          </md-card-expand-trigger>
        </md-card-actions>
        <md-card-expand-content>
          <md-content>
            <p >{{ dessert.description }}</p>
          </md-content>
        </md-card-expand-content>
      </md-card-expand>
    </md-ripple>
  </md-card>
  <!-- </div> -->
</template>

<script>
export default {
  name: "Dessert",
  props: ["dessert"],
  computed: {
    stock: function() {
      return this.dessert.inventory < 5
        ? `Only ${this.dessert.inventory} left in stock!`
        : "";
    }
  },
  methods: {
    addCart(dessert) {
      this.$emit("add", dessert);
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
.md-card {
  width: 350px;
  margin: 4px 10px;
  display: inline-block;
  // vertical-align: top;
  // display: flex;
}

// .price {
//   font: 50px;
// }
</style>
