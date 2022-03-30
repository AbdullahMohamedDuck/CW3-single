<template>
  <div id="app">
    <header>
      <h1>{{sitename}}</h1>
      <button class="buttonstyle" v-if="cart.length > 0" v-on:click='showCheckout'> {{cart.length}} <span class="fas fa-shopping-cart"></span>Cart</button>
    </header>
    

    <main>
      <div class="card-container">
        <div v-if='showProduct == true'>
         
    <div> <product-list :products='products' @addProduct='addItem' > </product-list> </div>
    </div>
        </div>

        <div v-if='showProduct == false'>
    
    <checkout :cart='cart' @removeProduct='removeFromCart' @showCheckout='showCheckout' > </checkout>
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
      cart: [],
      products:[],
    }

  },
  mounted() {
    fetch("https://cst3145cw2-single.herokuapp.com/collection/products").then(response => response.json()).then(
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
  

.subjectborder{
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
    width: 150px;
    height: 150px;
}

.styles {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
  }
 header{
    background: #cfcdcdb6;
    display: flex;
    justify-content: space-between;
    align-items: center;
    text-align: center;
    border-bottom: #1aaaec 7px solid;

}
.buttonstyle{
    width: 140px;
    height: 50px;
    background-color: #FFFFFF	;

}
.sortbyflex{
    margin: auto;
    width: 70%;
    padding: 10 px;
 
}
.card-container {
    margin: auto;
    width: 60%;
    padding: 10px;
    
  }
  .productList {
    display: inline-block;
    margin-left: 100px;
    margin-top: 50px;
}
  </style>
