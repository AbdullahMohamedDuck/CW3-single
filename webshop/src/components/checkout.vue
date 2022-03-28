<template>

    <div>
    <h2>Checkout</h2>
    <h3>Added products</h3>
    <div v-for='product in cart' :key="product.id">
        <img v-bind:src='product.image' alt="" width="100px" height="100px">
                            <br>
                            {{product.topic}} <br>
                            Location: {{product.location}} <br>
                            Price: £{{product.price}} <br>
    <button @click='removeFromCart(product)'>remove</button>
    </div>
    <p>
    <strong> Name </strong> <input v-model="name" />
    <strong> Address </strong> <input v-model="address" />
    <button> Submit </button>
    </p>
    </div>

</template>

<script> 

export default{
    name: 'form-checkout',
    props: ['cart'],
    data(){
        return{
            name: "",
            address: "",
        }
    },
    methods: {
    removeFromCart(product){
        this.$emit('removeProduct', product)
    },
   
    }
}

</script>