<template>
  <div>
    <div v-if="!submitted" class="payment">
      <h1>This is the checkout component</h1>
      <h2>Please give us your payment details:</h2>

      <label for="email">Email</label>
      <br />
      <input id="email" type="email" v-model="stripeEmail" placeholder="name@example.com" />
      <br />
      <br />
      <label for="card">Credit Card</label>
      <card
        id="card"
        :class="{ complete }"
        stripe="pk_test_5ThYi0UvX3xwoNdgxxxTxxrG"
        :options="stripeOptions"
        @change="complete = $event.complete"
      />
      <br />
      <button class="pay-with-stripe" @click="pay" :disabled="!complete">Pay with credit card</button>

      <p>
        Test using this credit card:
        <span class="cc-number">4242 4242 4242 4242</span>, and enter any 5 digits for the zip code
      </p>
    </div>
    <div v-if="status === 'failure'">
      <h3>Oh No!</h3>
      <p>Something went wrong!</p>
      <button @click="clearCheckout">Please try again</button>
    </div>
    <div v-if="status === 'success'">
      <h3>Congrats! Your Payment Went Through</h3>
    </div>
  </div>
</template>

<script>
//import { stripeKey, stripeOptions } from './stripeConfig.json';
import { Card, createToken } from "vue-stripe-elements-plus";
import axios from "axios";

export default {
  name: "Checkout",
  components: {
    Card
  },

  props: {
    total: {
      type: [Number, String],
      default: "50.00"
    },
    success: {
      type: Boolean,
      default: false
    }
  },

  data() {
    return {
      submitted: false,
      complete: false,
      status: "",
      response: "",
      stripeOptions: {
        // you can configure that cc element. I liked the default, but you can
        // see https://stripe.com/docs/stripe.js#element-options for details
      },
      stripeEmail: ""
    };
  },

  methods: {
    pay() {
      // createToken returns a Promise which resolves in a result object with
      // either a token or an error key.
      // See https://stripe.com/docs/api#tokens for the token object.
      // See https://stripe.com/docs/api#errors for the error object.
      // More general https://stripe.com/docs/stripe.js#stripe-create-token.
      createToken().then(data => {
        this.submitted = true; // we'll change the flag to let ourselves know it was submitted
        console.log(data.token); // this is a token we would use for the stripeToken below
        axios
          .post(
            "https://sdras-stripe.azurewebsites.net/api/charge?code=zWwbn6LLqMxuyvwbWpTFXdRxFd7a27KCRCEseL7zEqbM9ijAgj1c1w==",
            {
              stripeEmail: this.stripeEmail, // send the email
              stripeToken: data.token.id, // testing token
              stripeAmt: this.total // send the amount
            },
            {
              headers: {
                "Content-Type": "application/json"
              }
            }
          )
          .then(response => {
            this.status = "success";
            this.$emit("successSubmit");
            this.$store.commit("clearCartCount");
            // console logs for you :)
            this.response = JSON.stringify(response, null, 2);
            console.log(this.response);
          })
          .catch(error => {
            this.status = "failure";
            // console logs for you :)
            this.response = "Error: " + JSON.stringify(error, null, 2);
            console.log(this.response);
          });
      });
    },
    clearCheckout() {
      this.submitted = false;
      this.status = "";
      this.complete = false;
      this.response = "";
    }
  }
};
</script>

<style scoped>
h1 {
  color: #f0a812;
  text-align: center;
}
h2 {
  color: #f0a812;
  text-align: center;
}
.stripe-card {
  width: 300px;
  border: 1px solid grey;
}
.stripe-card.complete {
  border-color: green;
}
</style>