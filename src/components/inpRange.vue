<script setup>
import { computed, ref } from 'vue';

  const props=defineProps(["min","max","value", "bgColor"])

  const emit=defineEmits(["update:modelValue"])

  const value=ref(props.value)

const bar = ref(null)
  const top=computed(()=>{
    return ((value.value - props.min) / (props.max - props.min)) * 100
  })


const updateValue = (e) => {
    const rect = bar.value.getBoundingClientRect()

    const y = e.clientY - rect.top
    let percent =  y / rect.height

    percent = Math.max(0, Math.min(1, percent))

  const min = props.min
  const max = props.max

  value.value = min + percent * (max - min)
  
  emit('update:modelValue', value.value)
}

const startDrag=(e)=>{

  updateValue(e)

  const move = (e) => updateValue(e)

  const stop = () => {
    window.removeEventListener('pointermove', move)
    window.removeEventListener('pointerup', stop)
  }

  window.addEventListener('pointermove', move)
  window.addEventListener('pointerup', stop)
}


const background=computed(()=>({
  background:props.bgColor
}))


</script>

<template>

  <div class="bar" ref="bar" :style="background" @pointerdown="startDrag">
    <div class="circle" :style="{top: `calc(${top}% - 9px)`}"></div>
  </div>


</template>

<style scoped>

  .bar{
    height: 100%;
    width: 20px;
    overflow-y: hidden;
    padding-inline:1px;
    position: relative;
  }

  .circle{
    background-color: black;
    border-radius: 100%;
    width: 18px;
    height: 18px;
    
    left: 2px;
    
    position: absolute;
  }


</style>