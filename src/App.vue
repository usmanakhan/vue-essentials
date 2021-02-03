<template>
  <div id="app" class="container mt-5">
    <router-view
      :cart="cart" 
      :cartQty="cartQty" 
      :cartTotal="cartTotal" 
      :sliderStatus="sliderStatus" 
      :maximum.sync="maximum"
      :products="products" 
      
      @delete="deleteItem"
      @toggle="toggleSliderStatus" 
      @add="addItem"
    ></router-view>
    
  
  </div>
</template>

<script>
//import {FontAwesomeIcon} from '@fortawesome/vue-fontawesome';
//import Products from './components/Products.vue';
//import Checkout from './components/Checkout.vue';

export default {
  name: 'App',
  data:function(){
    return{
    maximum: 99,
    sliderStatus: true,
    products: null,
    cart:[]
    }

  },
  components: {
    
    //Products, Checkout
  },
  
  methods:{
    toggleSliderStatus : function(){
      this.sliderStatus = !this.sliderStatus
    },
    addItem : function(product){
      //this.cart.push(product)
      var witchProduct;
      var existing = this.cart.filter(function(item, index){
        if(item.product.id == Number(product.id)){
          witchProduct = index;  
          return true
        }else{
          return false
        }
      });
      
      if(existing.length){
        this.cart[witchProduct].qty++
      }else{
        this.cart.push({product:product, qty:1})
      }
    },
    deleteItem : function(id){
      if(this.cart[id].qty > 1){
        this.cart[id].qty--;
      }else{
        this.cart.splice(id,1);
      }
    }
    
  },
  computed: {
    cartQty: function(){
      let qty  = 0;
      let item;
      for(item in this.cart){
        qty = qty + this.cart[item].qty
      }
      return qty
    },
    cartTotal: function(){
      let sum  = 0;
      let item;
      for(item in this.cart){
        sum = sum+(this.cart[item].product.price * this.cart[item].qty)
      }
      return sum
    },
    
  },
  filters: {
    currency : function(value){
      return '$'+Number.parseFloat(value).toFixed(2)
    }
  },
  mounted: function() {
    fetch('https://hplussport.com/api/products/order/price')
    .then(response => response.json())
    .then(data => {
      this.products = data;
    })
  }
}
</script>


