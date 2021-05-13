<template>
  <div class="home">
    <div class="feature-card">
      <router-link to="/movie/tt4154796">
      <img src="https://m.media-amazon.com/images/M/MV5BMTc5MDE2ODcwNV5BMl5BanBnXkFtZTgwMzI2NzQ2NzM@._V1_SX300.jpg" alt="Avengers EndGame" class="featured-img">
        <div class="detail">
          <h3> Avengers EndGame </h3>
          <p>After the devastating events of Avengers: Infinity War (2018), the universe is in ruins. With the help of remaining allies, the Avengers assemble once more in order to reverse Thanos' actions and restore balance to the universe.","Language":"English, Japanese, Xhosa, German</p>
        </div>
      </router-link>
    </div>
      <form @submit.prevent="searchMovies()" class="search-box">
        <input type="text" placeholder="Cosa stai cercando?" v-model="search"/>
        <input type="submit" value="Search" />
      </form>
    <div class="movies-list">
      <div class="movie" v-for="movie in movies" :key="movie.imdbID">
        <router-link :to=" '/movie/' + movie.imdbID" class="movie-link">
          <div class="product-image">
            <img :src="movie.Poster" alt="Film Poster" />
            <div class="type">{{movie.Type}} 
            </div>
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
// @ is an alias to /src
//import HelloWorld from '@/components/HelloWorld.vue'
import {ref} from 'vue';
import env from '@/env.js';
export default {
  setup(){
    const search = ref("");
    const movies = ref([]);

    const searchMovies = () => {
      if (search.value != ""){
        fetch(`http://www.omdbapi.com/?apikey=${env.apikey}&s=${search.value}`)
        .then(response => response.json())
        .then(data => {
          //console.log(data);
          movies.value = data.Search;
          search.value = ""
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
  .feature-card {
    position:relative;

    .featured-img{
      display: block;
      width: 100%;
      height: 400px;
      object-fit: cover;

      position: relative;
      z-index: 0;

    }

    .detail {
      position: absolute;
      left:0;
      right:0;
      bottom: 0;
      background-color: rgba($color: #000000, $alpha: 0.6);
      padding: 16px;
      z-index: 1;
    }  

    h3 {
      color: #fff;
      margin-bottom: 16px;
    }

    p{
      color:#FFF

    }
  }

  .search-box {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    padding: 16px;

    input {
      display: block;
      appearance:none;
      border: none;
      outline: none;
      background: none;

      &[type="text"]{
        width:100%;
        color: white;
        background-color: gray;
        font-size: 20px;
        padding: 5px 16px;
        border-radius: 8px;
        margin-bottom: 15px;
        transition: 0.4s;


        &::placeholder{
          color: white
        }

        &:focus {
          box-shadow: 0px 3px 6px rgba($color: #000000, $alpha: 0.2)
        }
      }

      &[type="submit"]{
        width: 100%;
        max-width: 300px;
        background-color: royalblue;
        padding: 16px;
        border-radius: 8px;
        color: #FFF;
        font-size: 20px;
        text-transform: uppercase;
        transition: 0.4s;

        &:active {
          background-color: blue;
        }
      }  

    }

  }

    .movies-list {
    display: flex;
    flex-wrap: wrap;
    margin: 0px 8px;
    .movie {
      max-width: 50%;
      flex: 1 1 50%;
      padding: 16px 8px;
      .movie-link {
        display: flex;
        flex-direction: column;
        height: 100%;
        .product-image {
          position: relative;
          display: block;
          img {
            display: block;
            width: 100%;
            height: 275px;
            object-fit: cover;
          }
          .type {
            position: absolute;
            padding: 8px 16px;
            background-color: #42B883;
            color: #FFF;
            bottom: 16px;
            left: 0px;
            text-transform: capitalize;
          }
        }
        .detail {
          background-color: #496583;
          padding: 16px 8px;
          flex: 1 1 100%;
          border-radius: 0px 0px 8px 8px;
          .year {
            color: #AAA;
            font-size: 14px;
          }
          h3 {
            color: #FFF;
            font-weight: 600;
            font-size: 18px;
          }
        }
      }
    }
  }

}
</style>
