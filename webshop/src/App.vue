<template>
  <div id="app">
    <header>
      <h1>{{sitename}}</h1>
      <button @click="showCheckout">{{this.cart.length}} Checkout</button>
    </header>
  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  // components: {
  //   HelloWorld
  // },
  data() {
    return {
      sitename: 'Vue.js Lesson Shop',
      cart: [],
    }
  },
  methods: {
 showCheckout() {
    this.showProduct = this.showProduct ? false : true;
    if (this.showProduct == false) {
    if (this.cart.length > 0) {

    this.order.productID = this.cart[0].productID;
    this.order.Spaces = this.cart[0].Spaces;
    console.log("Order", this.order);
      }
    }
                            
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
