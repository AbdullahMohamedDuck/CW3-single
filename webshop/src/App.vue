<template>
  <div id="app">
    <header>
      <h1>{{sitename}}</h1>
      <button @click="showCheckout">{{this.cart.length}} Checkout</button>
    </header>
    <product-list @addProduct='addToCart' > </product-list>
    <checkout :cart='cart' @removeProduct='removeFromCart'> </checkout>
  </div>
</template>

<script>
import productList from './components/productlist.vue'
import checkout from './components/checkout.vue'

export default {
  name: 'App',
  components: { productList, checkout },
  data() {
    return {
      sitename: 'Vue.js Lesson Shop',
      cart: [],
    }
  },
  methods: {
  showCheckout() {},
                            
  addToCart(product) {
    this.cart.push(product)
   },
   removeFromCart(product){
     let index = this.cart.indexOf(product);
      this.cart.splice(index, 1);
      product.Spaces++;
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
