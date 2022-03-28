<template>
  <div id="app">
    <header>
      <h1>{{sitename}}</h1>
      <button class="buttonstyle" v-if="cart.length > 0" v-on:click='showCheckout'> {{cart.length}} <span class="fas fa-shopping-cart"></span>Cart</button>
    </header>
    

    <main>
        <div v-if='showProduct == true'>
    <product-list :products='products' @addProduct='addItem' > </product-list>
        </div>

        <div v-if='showProduct == false'>
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
      showProduct: true,
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
                product.Spaces--;
            },
            
        showCheckout() {
            this.showProduct = this.showProduct ? false : true;
            
        },
        

      removeFromCart(product) {
          let index = this.cart.indexOf(product);
          this.cart.splice(index, 1);
          product.Spaces++

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
  

/* .subjectborder{
    width: 210px;
    background-color: #91c7fa;
    padding: 20px 20px;
    margin: 15px;
    border-radius: 10px;
    
    
}
.subjectborder figure{
    display: flex;
    justify-content: center;
    align-items: right;
    flex-wrap: wrap;
}
.subjectborder figure img{
    width: 100px;
    height: 100px;
} */
 
  </style>
