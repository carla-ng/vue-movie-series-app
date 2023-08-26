<template>
  <div class="movie-detail">
    <h2>{{movie.Title}}</h2>
    <p>{{ movie.Year }}</p>
    <div class="img-plot">
      <img :src="movie.Poster" alt="Movie Poster" class="featured-img" />
      <p>{{ movie.Plot }}</p>
    </div>
    <div class="more-info">
      <p><span>Director:</span> {{ movie.Director }}</p>
      <p><span>Actors:</span> {{ movie.Actors }}</p>
      <p><span>Country:</span> {{ movie.Country }}</p>
      <p><span>IMDB Rating:</span> {{ movie.imdbRating }} / 10</p>
    </div>
  </div>
</template>

<script>
import { ref, onBeforeMount } from 'vue';
import { useRoute } from 'vue-router';
import env from '@/env.js';

export default {
  setup () {
    const movie = ref({});
    const route = useRoute();

    onBeforeMount(() => {
      fetch(`https://www.omdbapi.com/?apikey=${env.apikey}&i=${route.params.id}&plot=full`)
        .then(response => response.json())
        .then(data => {
          movie.value = data;
          console.log(data);
        });
    })

    return {
      movie
    }

  }
}
</script>

<style lang="scss">
.movie-detail {
  margin: 0 auto;
  max-width: 1000px;
  padding: 36px 16px;

  h2 {
    color: #FFF;
    font-size: 28px;
    font-weight: 600;
    margin-bottom: 16px;
  }

  p {
    color: #FFF;
    font-size: 18px;
    line-height: 1.4;
    }

  .img-plot {
    @media only screen and (min-width: 992px) {
      display: flex;
      flex-direction: row;
    }

    .featured-img {
      display: block;
      margin: 16px 0;
      max-width: 200px;
    }

    p {
      @media only screen and (min-width: 992px) { margin: 16px; }
    }
  }

  .more-info {
    margin-top: 20px;
    @media only screen and (min-width: 992px) { margin-top: 10px; }

    p {
      span {
        font-weight: bold;
        margin-right: 8px;
      }
    }
  }
}
</style>