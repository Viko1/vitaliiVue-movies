<template>
    <div class="movie-detail">
        <h2>{{movie.Title}}</h2>
        <p>{{movie.Year}}</p>
        <img :src="movie.Poster" alt="Movie Poster" class="featured-img"/>
        <p>{{ movie.Plot}}</p>
    </div>
</template>

<script>
   import {ref, onBeforeMount} from 'vue';
   import {useRoute} from 'vue-router'
   import env from '../env'

   export default {
      setup() {
         const movie = ref({});
         const route = useRoute();

         onBeforeMount(() => {
            fetch(`http://www.omdbapi.com/?apikey=${env.apikey}&i=${route.params.id}&plot=full`)
               .then(response => response.json())
               .then(data => {
                  movie.value = data
               })
         })

         return {
            movie
         }

      }
   }
</script>

<style lang="scss">
    .movie-detail {
        width: 50%;
        position: relative;
        left: 50%;
        transform: translate(-50%, 0);
        padding: 16px;

        h2 {
            position: relative;
            left: 50%;
            transform: translate(-50%, 0);
            color: white;
            text-align: center;
            font-size: 28px;
            margin-bottom: 16px;
            font-weight: 600;
        }

        .featured-img {
            display: block;
            position: relative;
            left: 50%;
            max-width: 100%;
            margin-bottom: 16px;
            transform: translate(-50%, 0);
        }

        p {
            position: relative;
            text-align: center;
            left: 50%;
            transform: translate(-50%, 0);
            color: #FFF;
            font-size: 18px;
            line-height: 1.5;
        }


    }

    @media only screen and (max-width: 600px) {
        .movie-detail {
            width: 100% !important;
            position: relative;
            left: 50%;
            transform: translate(-50%, 0);
            padding: 16px;
        }
    }

</style>