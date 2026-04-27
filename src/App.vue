<script setup lang="js">
import { computed, ref } from 'vue';
import Color from './components/color.vue';
import Guesser from './components/Guesser.vue';
import CountDown from './components/countDown.vue';

  const GameState={
    showColor:"showColor",
    guessing:"guessing",
    showResult:"showResult"

  }


  const game=ref({

    realColor:{
      h:Math.random()*360,
      s:Math.random()*90+10,
      b:Math.random()*90+10

    },
    actualColor:{
      h:Math.random()*360,
      s:Math.random()*90+10,
      b:Math.random()*90+10
    },
    gameState:GameState.showColor

  })


const actualColor = computed(() => ({
  hue: game.value.actualColor.h,
  saturation: game.value.actualColor.s,
  brightness: game.value.b
}))



</script>

<template>
  <section style="display: flex; flex-direction:row; justify-content: center; align-items: center; height: 100vh; ">

    <Color v-if="game.gameState==GameState.showColor" :hue="game.realColor.h" :saturation="game.realColor.s" :brightness="game.realColor.b">
      <CountDown time="5000" @timeEnded="game.gameState=GameState.guessing"/>
    </Color> 


    <Color v-else-if="game.gameState==GameState.guessing" :hue="game.actualColor.h" :saturation="game.actualColor.s" :brightness="game.actualColor.b">
        <Guesser v-model:hue="game.actualColor.h" v-model:saturation="game.actualColor.s" v-model:brightness="game.actualColor.b" @guess="console.log('actual:',game.actualColor);console.log('real:',game.realColor);game.showingColor=true"/>
    </Color> 

  </section>
</template>

<style scoped>



</style>
