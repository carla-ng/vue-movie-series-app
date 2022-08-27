<template>
  <div class="home">

    <div class="featured-card">
      <router-link to="/movie/tt0221735">
         <img src="https://m.media-amazon.com/images/M/MV5BYThkZTBiN2UtZWJkMC00NzQ1LTg4ODktYjlhN2UwMTYzZWVhXkEyXkFqcGdeQXVyNjk1Njg5NTA@._V1_SX1000.jpg"
          alt="Home Poster" class="featured-img">
          <div class="detail">
            <h3>Series and Movie app</h3>
            <p>Find information about any movie or series.</p>
          </div>
      </router-link>
    </div>

    <form @submit.prevent="searchMovies()" class="search-box">
      <input type="text" placeholder="What are you looking for?" v-model="search" />
      <input type="submit" value="Search" />
    </form>

    <div class="movies-list">
      <div class="movie" v-for="movie in movies" :key="movie.imdbID">

        <router-link :to="'/movie/' + movie.imdbID" class="movie-link">
          <div class="product-image">
            <img :src="movie.Poster" alt="Movie Poster" />
            <div class="type">{{ movie.Type }}</div>
          </div>

          <div class="detail">
            <p class="year">{{ movie.Year }}</p>
            <h3>{{ movie.Title }}</h3>
          </div>
        </router-link>

      </div>
    </div>

  </div>
</template>

<script>
import { ref } from 'vue';
import env from '@/env.js'

export default {
  setup() {
    const search = ref("");
    const movies = ref([]);

    const searchMovies = () => {
      if ( search.value != "" ) {
        fetch(`http://www.omdbapi.com/?apikey=${env.apikey}&s=${search.value}`)
          .then( response => response.json() )
          .then( data => {
            movies.value = data.Search;
            search.value = "";
          })
      }
    }

    return {
      search,
      movies,
      searchMovies
    }
  }
}
</script>

<style lang="scss">
.home {
  margin: 0 auto;
  max-width: 1300px;

  .featured-card {
    position: relative;

    .featured-img {
      display: block;
      height: 300px;
      object-fit: cover;
      object-position: top;
      position: relative;
      width: 100%;
      z-index: 0;
    }

    .detail {
      background-color: rgba(0, 0, 0, 0.6);
      bottom: 0;
      left: 0;
      padding: 16px;
      position: absolute;
      right: 0;
      z-index: 1;

      h3 {
        color:#fff;
        margin-bottom: 16px;
      }

      p { color: #fff; }
    }

  }

  .search-box {
    display: flex;
    align-items: center;
    flex-direction: column;
    justify-content: center;

    margin: 0 auto;
    max-width: 800px;
    padding: 16px;

    @media only screen and (min-width: 992px) { padding: 25px 16px; }

    input {
      appearance: none;
      background: none;
      border: none;
      display: block;
      outline: none;

      &[type="text"] {
        background-color: #565656;
        border-radius: 8px;
        color: #fff;
        font-size: 20px;
        margin-bottom: 15px;
        padding: 10px 16px;
        transition: 0.4s;
        width: 100%;

        &::placeholder { color: #f3f3f3; }
        &:focus { box-shadow: 0px 3px 6px rgba(0, 0, 0, 0.2); }
      }

      &[type="submit"] {
        width: 100%;
        max-width: 300px;
        background-color: #e91e63;
        padding: 16px;
        border-radius: 8px;
        color: #FFF;
        font-size: 20px;
        text-transform: uppercase;
        transition: 0.4s;

        &:active { background-color: #a10037; }
      }
    }

  }

  .movies-list {
    display: flex;
    flex-wrap: wrap;
    margin: 16px auto;
    max-width: 1200px;

    @media only screen and (min-width: 992px) { margin: 30px auto; }

    .movie {
      flex: 1 1 50%;
      max-width: 50%;
      padding: 16px 8px;

      @media only screen and (min-width: 992px) {
        flex: 1 1 25%;
        max-width: 25%;
      }

      .movie-link {
        display: flex;
        flex-direction: column;
        height: 100%;

        .product-image {
          display: block;
          position: relative;

          img {
            display: block;
            height: 275px;
            object-fit: cover;
            object-position: top;
            width: 100%;
          }

          .type {
            background-color: #e91e63;
            bottom: 0;
            color: #FFF;
            left: 0px;
            padding: 6px 12px;
            position: absolute;
            text-transform: capitalize;
          }
        }

        .detail {
          background-color: #000;
          border-radius: 0px 0px 8px 8px;
          flex: 1 1 100%;
          padding: 16px 8px;

          .year {
            color: #aaa;
            font-size: 14px;
          }

          h3 {
            color: #FfffFF;
            font-size: 18px;
            font-weight: 600;
            margin-top: 3px;

            overflow: hidden;
            text-overflow: ellipsis;
            display: -webkit-box;
            -webkit-line-clamp: 3;
                    line-clamp: 3;
            -webkit-box-orient: vertical;
          }
        }
      }
    }
  }
  
}
</style>
