<template>
    <main>
        
        <div v-for="product in products" :key="product.id">
     <figure>
        <img v-bind:src='product.image'>
        </figure>
        <h2>{{product.topic}}</h2>
        <p>Lesson ID: {{product.id}}</p>
        <p>Description: {{product.description}}</p>
        <p>Location: {{product.location}}</p>
        <p>Price: £{{product.price}}</p>
        <p>Spaces: {{product.Spaces }}</p>
        <button @click="addToCart(product)">Add to cart</button>   
        </div>
    </main>
</template>

<script>
export default {
    name: 'ProductList',
    data(){
        return {
            products:[
                {
                    "id":1001,
                    "topic":"Subject: Maths",
                    "description":"Learn maths with this subject",
                    "price":99,
                    "location": "London",
                    "image":"maths.jpg", 
                    "Spaces":5   
                }
            ]
        }
    },

    // mounted() {
    //     fetch(this.apiUrl + "collection/products").then(response => response.json()).then(
    //         data => {
    //             this.products = data;
    //         });
    // },
    methods: {
        addToCart(product) {
        this.$emit('addProduct', product)
        //product.Spaces--
    }
    }
}

</script>
