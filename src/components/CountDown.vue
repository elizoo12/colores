<script setup>
import { ref,defineEmits,defineProps } from 'vue';


const props=defineProps(["time"])
const emits=defineEmits(["timeEnded"])

  const t=ref(props.time)
  
const interval = setInterval(() => {
  t.value -= 10
  if (t.value <= 0) {
    t.value = 0 
    clearInterval(interval)
    emits('timeEnded')
  }
}, 10)




</script>


<template>
  <div style="width: 100%; height: 100%; position: relative;">

  <p style="font-size: larger;color: white; position: absolute; top: 10px; right: 10px; margin: 0;" >{{t}}</p>

  </div>

</template>