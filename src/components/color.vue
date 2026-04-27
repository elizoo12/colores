<script setup>
import { computed, ref } from 'vue';
import HSVtoRGB from "../utils/HSB_RGB.js"

  
  const props=defineProps(["hue","saturation","brightness"])
  

  const ancho=window.innerWidth*0.7;
  const alto=window.innerHeight;
  const proporcion=9/16;


  const estiloCaja=computed(()=>{
    
    let color=HSVtoRGB(props.hue,props.saturation,props.brightness)
    return{

    width:ancho*proporcion+"px",
    height:alto*proporcion+"px",
    backgroundColor: `rgb(${color.r},${color.g},${color.b})`,
    "border-radius":"10px",
    overflow:"hidden"
  }})


  

</script>


<template>
  <div>
    <div :style="estiloCaja">
      <slot></slot>
    </div>
  </div>
</template>


<style scoped>

</style>