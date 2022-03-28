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
    <product-list :products='products' @addProduct='addItem' id="style1" > </product-list>
        </div>
        <div else>
    <checkout :cart='cart' @removeProduct='removeFromCart'> </checkout>
        </div>
    </main>

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
  addItem(product) {
          this.cart.push(product)
          product.Spaces--
      },


      showCheckout() {
          this.showProduct = this.showProduct ? false : true;
          if (this.showProduct == false) {
              if (this.cart.length > 0) {

                  this.order.productID = this.cart[0].productID;
                  this.order.Spaces = this.cart[0].Spaces;
                  console.log("Order", this.order);
              }
          }
      },



      removeFromCart(product) {
          let index = this.cart.indexOf(product);
          this.cart.splice(index, 1);
          product.Spaces++

      },

      backPage() {
          this.showProduct = this.showProduct ? false : true;
      },

      canAddToCart(product) {
          if (this.cart.length > 0) {
              if (product.productID != this.cart[0].productID) {
                  return false;
              }
              else {
                  return product.Spaces > 0;
              }
          }
          else {
              return product.Spaces > 0;
          }



      },


      // Sorting Function
      sort(s) {
          if (s === this.sortBy) {
              this.sortDir = this.sortDir === 'asc' ? 'desc' : 'asc';
          }
          this.sortBy = s;

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
  
#style1 {
    display: flex;
        margin-top: 0px;
    flex-wrap: wrap;
    margin: auto;
    width: 70%;
    padding: 10 px;
    gap: 10px;
    border: 5px solid rgb(181, 181, 202);
    background-color: rgb(159, 244, 255)
    
}

  </style>
