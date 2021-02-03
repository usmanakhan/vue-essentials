<template>
    <div>
        <h1>My Shop</h1>
        <navbar :cart="cart" :cartQty="cartQty" :cartTotal="cartTotal"></navbar>
        <p class="animate__animated animate__fadeInRight">take a look at our offerings bellow</p>
        <price-slider :sliderStatus="sliderStatus" :maximum.sync="maximum"></price-slider>
        <product-list :products="products" :maximum="maximum"></product-list>
        <font-awesome-icon icon="shopping-cart"></font-awesome-icon>
    </div>
</template>

<script>
import {FontAwesomeIcon} from '@fortawesome/vue-fontawesome';
import Navbar from './Navbar.vue';
import PriceSlider from './PriceSlider.vue';
import  ProductList from './ProductList.vue';
export default {
    name: "products",
    props:[
        "products",
        "maximum",
        "cart",
        "cartQty",
        "cartTotal",
        "sliderStatus",
        "sliderState"
    ],
    components:{
       FontAwesomeIcon,  Navbar, PriceSlider, ProductList
    }
        

    
}
</script>
