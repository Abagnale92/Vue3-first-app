<template>
  <div class="movie-detail">
       <h2>{{movie.Title}}</h2>
       <p>{{movie.Production}}</p>
    <img :src="movie.Poster" alt="Film Poster" />
    <p>Writer: {{movie.Writer}}</p> 
    <hr>
    <p>{{movie.Plot}}</p>
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
      fetch(`http://www.omdbapi.com/?apikey=${env.apikey}&i=${route.params.id}&plot=full`)
        .then(response => response.json())
        .then(data => {
          movie.value = data;
          console.log(movie.value)
        });
    });
    return {
      movie
    }
  }
}
</script>

<style lang="scss">
.movie-detail {
  padding: 16px;
  h2 {
    color: #FFF;
    font-size: 28px;
    font-weight: 600;
    margin-bottom: 16px;
    text-align: center;
  }

  img{
      display: block;
      margin:0px auto;
      text-align: center;
  }
  
  p {
    color: #FFF;
    font-size: 14px;
    line-height: 1.4;
  }
}
</style>