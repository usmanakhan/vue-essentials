<template>
  <transition name="custom-classes-transition"
    enter-active-class="animate__animated animate__fadeInDown" leave-active-class="animate__animated animate__fadeOutUp"          >
    <div v-if="sliderStatus">
      <div class="align-items-center" :class="sliderState">
        <label :class="labelCSS" for="formMax">max</label>
        <input type="text" @change="$parent.$emit('update:maximum',maxAmount)" id="formMax" class="form-control mx-2 text-center" style="width:60px" v-model="maxAmount"/>  
      <input type="range" @input="$parent.$emit('update:maximum',maxAmount)" class="custom-range" min="0" max="200" v-model="maxAmount" />
      </div>
    </div>
  </transition>
</template>

<script>
export default {
    name: "price-slider",
    props:["sliderStatus"],
    data:function(){
        return{
            maxAmount:99,
            labelCSS : ['form-weight-bold', 'mr-2']
        }
    },
    
    computed:{
        sliderState : function(){
            return this.sliderStatus ? 'd-flex' : 'd-none';
        }
    }
}
</script>

<style>

</style>
