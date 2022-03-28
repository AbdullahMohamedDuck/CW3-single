<template>
    <main>
        
        <div v-for="product in products" :key="product.id">
     <figure>
        <img v-bind:src='product.image' alt="" width="200px" height="200px">
        </figure>
        <h2>{{product.topic}}</h2>
        <p>Description: {{product.description}}</p>
        <p>Location: {{product.location}}</p>
        <p>Price: £{{product.price}}</p>
        <p>Spaces: {{product.Spaces }}</p>
        
        <button @click='addItem(product)'><span class="fas fa-shopping-basket"></span>Add to cart</button>
        
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
      


    }
}

</script>
