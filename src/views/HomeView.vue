<template>
  <div class="w-full flex justify-center">
    <input
      type="text"
      :placeholder="placeholder"
      class="mt-10 p-2 border-blue-500 border-2"
      v-model="text"
    />
  </div>

  <div class="mt-10 p-4 flex flex-wrap justify-center">
    <div class="ml-4 text-2xl text-blue-500"
         v-for="(pokemon, idx) in filteredPokemon"
         :key="idx">
      <router-link :to='`/about/${urlIdLookup[pokemon.name]}`'>
        {{ pokemon.name }}
      </router-link>
    </div>
  </div>
</template>

<script>
import {reactive, toRefs, computed} from "vue";

export default {
  name: 'HomeView',
  setup(){
    const state = reactive({
      pokemons: [],
      urlIdLookup: {},
      text: '',
      filteredPokemon: computed(() => updatePokemon()),
      placeholder: ''
    })
    function changeCase(){
      return  state.text.toLowerCase()
    }
    function updatePokemon(){
      if(!state.text) { return [] }
      return state.pokemons.filter((pokemon) => pokemon.name.includes(changeCase()))
    }

    fetch('https://pokeapi.co/api/v2/pokemon?limit=900&offset=0')
      .then((res) => res.json())
      .then((data) => {
        state.placeholder = data.results[Math.floor(Math.random() * 800)].name + '?'
        state.pokemons = data.results
        state.urlIdLookup = data.results.reduce((acc, cur, idx) =>
        acc = {...acc, [cur.name]:idx+1}
        ,{})
      })

      return { ...toRefs(state) }
  }
}
</script>
