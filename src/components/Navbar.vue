<template>
    <nav class="navbar navbar-light fixed-top  "  >
        <div class="navbar-text ml-auto d-flex">
            <button @click="$parent.$emit('toggle')" class="btn btn-sm btn-outline-success">
                <i class="fas fa-dollar-sign"></i>
                <font-awesome-icon icon="dollar-sign"></font-awesome-icon>
            </button>
            <div class="mx-2 dropdown" >
                <button class="btn btn-success btn-sm dropdown-toggle"
                        id="cartDropdown" data-toggle="dropdown" data-display="static" aria-haspopup="true" aria-expanded="false">
                    <span class="badge badge-pill badge-light">{{cartQty}}</span>
                <i class="fas fa-shopping-cart mx-2"></i>
                <font-awesome-icon icon="shopping-cart"></font-awesome-icon>
                
                {{cartTotal | currency}}
                </button>
                <div class="dropdown-menu dropdown-menu-right"
                    aria-labelledby="cartDropdown" v-if="cart.length > 0">
                
                    <div v-for="(item, index) in cart" :key="index">
                        <div class="dropdown-item-text text-nowrap text-right">
                        <span class="badge badge-pill badge-warning align-text-top mr-1">{{item.qty}}</span>
                        {{item.product.name}}
                        
                        <price :value="Number(item.qty * item.product.price)"></price>
                        <a href="#" @click.stop="$parent.$emit('delete',index)" class="badge badge-danger text-white">-</a>
                        </div>
                    </div>
                    <router-link class="btn btn-sm btn-outline-info text-dark float-right mr-4" to="/checkout">Checkout</router-link>
                </div>
                
            </div>
        </div>
    </nav>
</template>

<script>
import Price from "./Price.vue";
import {FontAwesomeIcon} from '@fortawesome/vue-fontawesome';
export default {
    name : "navbar",
    props: ["cart", "cartQty", "cartTotal"],
    components : {FontAwesomeIcon, Price},
    filters: {
        currency : function(value){
        return '$'+Number.parseFloat(value).toFixed(2)
        }
    }
}
</script>
