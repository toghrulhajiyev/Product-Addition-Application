<template>
    <div v-if="productList.length > 0">
        <h3 class="text-center">Added products list</h3>
        <hr>
        <div class="row product-container">
            <app-product v-for="product in productList" :key="product">
                <img class="card-img-top" :src="product.selectedImage" :alt="product.title">
                <div class="card-body">
                    <h5 class="card-title">{{ product.title }}</h5>
                    <small><strong>Count : </strong> {{ product.count }}</small>
                    <br>
                    <small><strong>Price : </strong> {{ product.price }}</small>
                    <br>
                    <small><strong>Total : </strong> {{ product.totalPrice }}</small> 
                </div>
            </app-product>
        </div>
    </div>
</template>

<script>
import Product from './Product.vue'
import { eventBus } from '../main.js'

export default {
    data() {
        return {
            productList: [],
        }
    },
    components: {
        appProduct: Product,
    },
    created() {
        eventBus.$on('addNewProduct', (data) => {
            if(this.productList.length < 10) {
                this.productList.push(data);
                eventBus.$emit('getProductLength', this.productList.length);
            } else {
                alert('You cannot add any product');
            }
        })
    }
}
</script>

<style>

</style>