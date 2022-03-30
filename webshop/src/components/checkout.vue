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
    <Strong>First name</Strong>
    <input v-model='order.firstName'>

    </p>

    <p>
        <Strong>Last name</Strong>
        <input v-model='order.lastName'>

    </p>

    <p>
        <Strong>Phone number</Strong>
        <input type="text" maxlength="11" v-model='order.phoneNumber'>

    </p>



    <h3>Order Information</h3>
    <p>First name: {{order.firstName}}</p>
    <p>Last name: {{order.lastName}}</p>
    <p>Phone number: {{order.phoneNumber}}</p>


    <button @Click="submitForm" :disabled="!orderFormCheck">Checkout</button>

    </div>

</template>

<script> 
/* eslint-disable */
export default{
    name: 'form-checkout',
    props: ['cart'],
    data(){
        return {
                  showProduct: "false",
            order: {
                    firstName: '',
                    lastName: '',
                    phoneNumber: '',
                    productID: "",
                    spaces: 0,
                },
            }
    },
    methods: {
        removeFromCart(product){
            this.$emit('removeProduct', product)
        },
        submitForm(){
            //post order first/last name, phone number, spaces, productID, 
            let order = {
                'productID': this.order.productID,
                'First Name': this.order.firstName,
                'Last Name': this.order.lastName,
                'Phone Number': this.order.phoneNumber,
                'Spaces': this.cart.length,
            }
            console.log(order);
            fetch("https://cst3145cw2-single.herokuapp.com/collection/OrderInfo", {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json',
                },
                body: JSON.stringify(order),
            }).then(function (response) {
                response.json().then(
                    console.log("Order Successfully posted to database")
                )
                alert("Order has been successfully placed!");

            })
            
            let updatedSpaces = { "Spaces": this.order.Spaces }

            fetch("https://cst3145cw2-single.herokuapp.com/collection/products" + this.order.productID, {
                method: 'PUT',
                headers: {
                    'Content-Type': 'application/json',
                },
                body: JSON.stringify(updatedSpaces),
            }).then((response) => {
                this.cart.splice(0);


                console.log("Updated spaces done!")

            })

        },
   
    },

    computed: {

        // Number/Name checker Function
        orderFormCheck() {
            let lettercheck = /^[a-z]+$/i;
            let numbercheck = /^[0-9]+$/i;
            if (lettercheck.test(this.order.firstName) &&
                lettercheck.test(this.order.lastName) && numbercheck.test(this.order.phoneNumber)) {
                this.order.correct = true;
            }
            else {
                this.order.correct = false;
            }
            return this.order.correct;
        },

        
    },
}

</script>