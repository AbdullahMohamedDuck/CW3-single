<template>
    <main>
        <div class="styles">
             <div class="sortbyflex">

    
            <!-- Start sorting ascending/descending -->
            <strong>Sort By</strong>
            <p><button @click="sort('topic')"><span class="fas fa-sort"></span></button> Topic</p>
            <p><button @click="sort('location')"><span class="fas fa-sort"></span></button> Location</p>
            <p><button @click="sort('price')"><span class="fas fa-sort"></span></button> Price</p>

        
      </div>
        <div  v-for="product in products" :key="product.id">
            <div class="subjectborder">
     <figure>
        <img v-bind:src='product.image'>
        </figure>
        <h2>{{product.topic}}</h2>
        <p>Lesson ID: {{product.productID}}</p>
        <p>Description: {{product.description}}</p>
        <p>Location: {{product.location}}</p>
        <p>Price: £{{product.price}}</p>
        <p>Spaces: {{product.Spaces }}</p>
        
        <button @click='addItem(product)' v-bind:disabled='!canAddToCart(product)'><span class="fas fa-shopping-basket"></span>Add to cart</button>
            </div>
        </div>
        </div>
    </main>
</template>

<script>
export default {
    name: 'ProductList',
    props: ['products'],
    data(){
        return {}
    },

    
    methods: {
        addItem(product) {
        this.$emit('addProduct', product)
    },
    
    canAddToCart(product) {
          if (this.cart > 0) {
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
