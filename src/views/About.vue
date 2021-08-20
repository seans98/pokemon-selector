<template>
  <div class="about">
    <div v-if="pokemon"
    class="w-4/12 m-auto bg-purple-100 mt-4 shadow-2xl flex justify-center flex-col items-center pb-4">
      <h3 class="text-2xl text-green-900 uppercase">{{pokemon.name}}</h3>
      <div class="flex justify-center">
        <img class="w-48" :src="pokemon.sprites.front_default" alt="">
        <img class="w-48" :src="pokemon.sprites.back_default" alt="">
      </div>
      <h3 class="text-yellow-400">Types</h3>
      <div v-for="(type, idx) in pokemon.types" :key="idx">
        <h3 class="text-sm font-medium bg-blue-300 py-1 px-2 rounded text-black-500 align-middle">{{type.type.name}}</h3>
      </div>
      <h3>Base Experience: <span class="text-sm font-medium bg-blue-300 py-1 px-2 rounded text-black-500 align-middle">{{pokemon.base_experience}} XP</span></h3>
      <h3>Height: <span class="text-sm font-medium bg-blue-300 py-1 px-2 rounded text-black-500 align-middle">{{pokemon.height}} m</span></h3>
      <h3>Abilities</h3>
      <div v-for="(ability,idx) in pokemon.abilities" :key="idx">
        <h3>{{ability.ability.name}}</h3>
      </div>
    </div>
  </div>
</template>
<script>
import { useRoute } from "vue-router";
import { reactive, toRefs } from "vue";
export default {
  setup() {
    const route = useRoute();
    const state = reactive({
      pokemon: null
    })
    fetch(`https://pokeapi.co/api/v2/pokemon/${route.params.slug}/`)
    .then((res)=> res.json())
    .then((data) => {
      console.log(data);
      state.pokemon = data;
    })
    return {... toRefs(state) }
  },
};
</script>
