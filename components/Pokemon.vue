<template>
  <div>
    <Pokemonnav />
    <div>
      <b-container fluid class="p-4">
        <b-row cols="1" cols-sm="2" cols-md="4" cols-lg="6">
          <div v-for="(item, index) in pokemon_list" :key="index">
            <b-card>
              <b-col>
                <b-img
                  thumbnail
                  fluid
                  :src="item.image"
                  alt="Image 1"
                  class="bg-dark"
                ></b-img>
                <h5 class="text-md-center">
                  {{ item.name }}
                </h5>
              </b-col></b-card
            >
          </div>
        </b-row>
      </b-container>
    </div>
  </div>
</template>
<script>
import axios from 'axios'
export default {
  data() {
    return {
      pokemon_list: [],
    }
  },
  async created() {
    var p = await axios.get(
      `https://pokeapi.co/api/v2/pokemon?limit=104&offset=0`
    )
    var pokemonname = p.data.results
    for (let index = 0; index < pokemonname.length; index++) {
      const element = pokemonname[index]

      var pokemonim = await axios.get(`${element.url}`)
      var pokemon_info = {
        name: element.name,
        image: pokemonim.data.sprites.other['official-artwork'].front_default,
      }
      this.pokemon_list.push(pokemon_info)
    }
    console.log(this.pokemon_list)
  },
}
</script>
