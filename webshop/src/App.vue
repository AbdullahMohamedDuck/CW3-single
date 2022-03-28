<template>
  <div id="app">
    <header>
      <h1>{{sitename}}</h1>
      
      <button @click="showCheckout">{{this.cart.length}} <span class="fas fa-shopping-cart"></span> Checkout</button>
    </header>
    

    <main>
        <div v-if="showCheckout">
            <div>                
            </div>
    <product-list :products='products' @addProduct='addToCart' > </product-list>
        </div>
        <div else>
    <checkout :cart='cart' @removeProduct='removeFromCart'> </checkout>
        </div>
    </main>
    <!-- <main>
     <div v-if="showCheckout">
           
     </div>
    <product-list :products='products' @addProduct='addToCart' > </product-list>
    <checkout :cart='cart' @removeProduct='removeFromCart'> </checkout>
  
    </main> -->
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
      apiUrl: 'https://cst3145cw2-single.herokuapp.com/',

      cart: [],
      products:[],
    }
  },
  mounted() {
    fetch(this.apiUrl + "collection/products").then(response => response.json()).then(
        data => {
            this.products = data;
        });
},
  methods: {
  showCheckout() {
   this.showProduct = this.showProduct ? false : true;

  },
                            
  addToCart(product) {
    this.cart.push(product)
    product.Spaces--

   },
   removeFromCart(product){
     let index = this.cart.indexOf(product);
      this.cart.splice(index, 1);
      product.Spaces++;
   },
   sortedProducts: function () 
        {
        return this.products.sort((a, b) => {
        let modifier = 1;
        if (this.sortDir === 'desc') modifier = -1;
        if (a[this.sortBy] < b[this.sortBy]) return -1 * modifier;
        if (a[this.sortBy] > b[this.sortBy]) return 1 * modifier;
        return 0;
        })

    },
  
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
