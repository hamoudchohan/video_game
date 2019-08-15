<template>
  <div class="container mx-auto">
    <div>{{game.name}}</div>
    <img :src="game.cover.url.replace('t_thumb','t_cover_big')" alt="cover" />
    <p>{{game.summary}}</p>
  </div>
</template>
<script>
import axios from "axios";

export default {
  asyncData({ params, error }) {
    return axios
      .get(
        `https://api-v3.igdb.com/games/${params.id}/?fields=name,cover.url,summary,platforms.name,first_release_date,websites,total_rating,screenshots.url,total_rating&expand=platforms,screenshots,cover`
      )
      .then(res => {
        return {
          game: res.data[0]
        };
      })
      .catch(e => {
        console.log(e);
      });
  }
};
</script>