<template>
  <div class="container mx-auto">
    <div class="game-container">
      <nuxt-link v-for="game in games" :key="game.id" class="block mb-8" :to="'/games/' + game.id">
        <img :src="game.cover.url.replace('t_thumb','t_cover_big')" alt="cover" />
        <div>{{game.name}}</div>
        <div v-for="genre in game.genres" :key="genre.id">{{genre.name}}</div>
      </nuxt-link>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  components: {},
  asyncData({ params, error }) {
    return axios
      .get(
        `https://api-v3.igdb.com/games/?fields=name,genres.name,cover.url,popularity&order=popularity:desc&expand=genres`
      )
      .then(res => {
        return {
          games: res.data
        };
      })
      .catch(e => {
        console.log(e);
      });
  },
  data() {
    return {
      games: []
    };
  }
};
</script>

<style>
/* Sample `apply` at-rules with Tailwind CSS
.container {
  @apply min-h-screen flex justify-center items-center text-center mx-auto;
}
*/
</style>
