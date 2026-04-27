<script setup>
import { computed, ref} from 'vue';
import InpRange from './inpRange.vue';
import HSVtoRGB from "../utils/HSB_RGB.js"



  const props=defineProps(["hue","brightness","saturation"])

  const emit = defineEmits([
  'update:hue',
  'update:saturation',
  'update:brightness',
  'guess'
])
  
  const bgColorS=computed(()=>{
    const color1=HSVtoRGB(props.hue,0,props.brightness)
    const color2=HSVtoRGB(props.hue,100,props.brightness)
    return `linear-gradient(rgb(${color1.r},${color1.g},${color1.b}) 0%, rgb(${color2.r},${color2.g},${color2.b}) 100%)`
  })

  const bgColorB=computed(()=>{

    const color1=HSVtoRGB(props.hue,props.saturation,0)
    const color2=HSVtoRGB(props.hue,props.saturation,100)
    return `linear-gradient(rgb(${color1.r},${color1.g},${color1.b}) 0%, rgb(${color2.r},${color2.g},${color2.b}) 100%)`
  })



</script>

<template>
  <div style="position: relative; height: 100%;">
    
    <div style="display: flex; flex-direction: row; height: 100%; ">

      <InpRange
        :min="0"
        :max="360"
        :value="props.hue"
        @update:modelValue="val => emit('update:hue', val)"
        :bgColor="' linear-gradient(rgb(255, 0, 0) 0%, rgb(255, 128, 0) 8.3%, rgb(255, 255, 0) 16.7%, rgb(128, 255, 0) 25%, rgb(0, 255, 0) 33.3%, rgb(0, 255, 128) 41.7%, rgb(0, 255, 255) 50%, rgb(0, 128, 255) 58.3%, rgb(0, 0, 255) 66.7%, rgb(128, 0, 255) 75%, rgb(255, 0, 255) 83.3%, rgb(255, 0, 128) 91.7%, rgb(255, 0, 0) 100%)'"
      />

      <InpRange
        :min="0"
        :max="100"
        :value="props.saturation"
        @update:modelValue="val => emit('update:saturation', val)"
        :bgColor="bgColorS"
      />

      <InpRange
        :min="0"
        :max="100"
        :value="props.brightness"
        @update:modelValue="val => emit('update:brightness', val)"
        :bgColor="bgColorB"
      />
    </div>

    <button style="position: absolute; bottom: 20px; right: 20px; background-color: white; border-radius: 100%; aspect-ratio: 1/1;" @click="emit('guess')"><img src="../assets/intentar.png" height="20px" width="20px" alt=""></button>

  </div>
</template>

<style>

</style>