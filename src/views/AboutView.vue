<template>
  <div class="about mx-4">
    <div v-if="pokemon" class="p-4 md:w-3/12  w-full m-auto bg-purple-100 mt-4 shadow-2xl flex justify-center flex-col items-center">

      <h3 class="text-2xl text-green-900 uppercase"> {{ pokemon.name }}</h3>
      <div v-if="isLoading" class="lds-ellipsis w-48 h-48"><div></div><div></div><div></div><div></div></div>
      <div v-else class="flex justify-center">
        <img  :class="{'w-48': !isLoading, 'h-48': !isLoading}" :src="pokemon.sprites.front_shiny" alt="">
        <img  :class="{'w-48': !isLoading, 'h-48': !isLoading}" :src="pokemon.sprites.back_shiny" alt="">
      </div>

      <div class="flex flex-row justify-around w-full">

        <div>
          <h3 class="text-yellow-400">Types</h3>
          <div v-for="(type, idx) in pokemon.types" :key="idx">
            <h5 class="text-blue-500">{{ type.type.name }}</h5>
          </div>
        </div>

        <div>
          <h3 class="text-red-400">Abilities</h3>
          <div v-for="(ability, idx) in pokemon.abilities" :key="idx">
            <h5 class="text-blue-500">{{ ability.ability.name }}</h5>
          </div>
        </div>

      </div>

    </div>
  </div>
</template>

<script>
import { useRoute } from 'vue-router'
import { reactive, toRefs } from "vue";
import axios from "axios";

export default {
  setup(){
    const header = window.document.body.querySelectorAll('a')[0]
    const route = useRoute()
    const state = reactive({
      pokemon: null,
      isLoading: true,
      colorCache: randomColor(),
    })

    async function getPokemon(){
      header.classList.add('scale')
      header.style.color = state.colorCache
      await
          axios
              .get(`https://pokeapi.co/api/v2/pokemon/${route.params.slug}/`)
              .then(response => { state.pokemon = response.data })
              .catch(e => alert(e))
      setTimeout(() =>{
        state.isLoading = false
        console.log(header.style.color)
      },500)
    }
    getPokemon()

    function randomColor() { return "#" + Math.floor(Math.random() * 16777215).toString(16) }
    randomColor()

    return { ...toRefs(state)}
  }
}
</script>
<style>
.lds-ellipsis {
  display: inline-block;
  position: relative;
  width: 80px;
  height: 80px;
}
.lds-ellipsis div {
  position: absolute;
  top: 33px;
  width: 13px;
  height: 13px;
  border-radius: 50%;
  background: salmon;
  animation-timing-function: cubic-bezier(0, 1, 1, 0);
}
.lds-ellipsis div:nth-child(1) {
  left: 8px;
  animation: lds-ellipsis1 0.6s infinite;
}
.lds-ellipsis div:nth-child(2) {
  left: 8px;
  animation: lds-ellipsis2 0.6s infinite;
}
.lds-ellipsis div:nth-child(3) {
  left: 32px;
  animation: lds-ellipsis2 0.6s infinite;
}
.lds-ellipsis div:nth-child(4) {
  left: 56px;
  animation: lds-ellipsis3 0.6s infinite;
}
@keyframes lds-ellipsis1 {
  0% {
    transform: scale(0);
  }
  100% {
    transform: scale(1);
  }
}
@keyframes lds-ellipsis3 {
  0% {
    transform: scale(1);
  }
  100% {
    transform: scale(0);
  }
}
@keyframes lds-ellipsis2 {
  0% {
    transform: translate(0, 0);
  }
  100% {
    transform: translate(24px, 0);
  }
}


.scale {
  font-weight: 500;
  animation-name: myanimation;
  animation-duration: 1.5s;
  animation-iteration-count: infinite;
}
@keyframes myanimation {
  0%   {
    -webkit-transform: scale(1);
    -moz-transform: scale(1);
    -o-transform: scale(1);
    -ms-transform: scale(1);
    transform: scale(1)
  }
  50%  {
    -webkit-transform: scale(1.1);
    -moz-transform: scale(1.1);
    -o-transform: scale(1.1);
    -ms-transform: scale(1.1);
    transform: scale(1.1)
  }
  100%  {
    -webkit-transform: scale(1);
    -moz-transform: scale(1);
    -o-transform: scale(1);
    -ms-transform: scale(1);
    transform: scale(1)
  }
}
</style>