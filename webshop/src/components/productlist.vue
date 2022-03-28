<template>
    <main>
        
        <div v-for="product in products" :key="product.id">
            <div class="subjectborder">
     <figure>
        <img v-bind:src='product.image' alt="" width="150px" height="150px">
        </figure>
        <h2>{{product.topic}}</h2>
        <p>Lesson ID: {{product.productID}}</p>
        <p>Description: {{product.description}}</p>
        <p>Location: {{product.location}}</p>
        <p>Price: £{{product.price}}</p>
        <p>Spaces: {{product.Spaces }}</p>
        
        <button @click='addItem(product)' ><span class="fas fa-shopping-basket"></span>Add to cart</button>
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


    }
}

</script>
