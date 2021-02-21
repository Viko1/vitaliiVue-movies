<template>
    <div class="home">
        <div class="feature-card">
            <router-link to="/movie/tt0137523">
                <img src="https://www.indiewire.com/wp-content/uploads/2021/01/fight-club.png" alt="Fight club poster"
                     class="featured-img">
                <div class="detail">
                    <h3>FIGHT CLUB</h3>
                    <p>
                        In this provocative drama co-starring Brad Pitt and Edward Norton
                        and directed by David Fincher, a disaffected man and his charismatic
                        friend organize brutal, bare-knuckle boxing matches.
                    </p>
                </div>
            </router-link>

        </div>
        <form @submit.prevent="SearchMovies()" class="search-box">
            <input type="text" placeholder="Write the name of the movie you would like to find" v-model="search">
            <input type="submit" value="Search"/>
        </form>

        <div class="movies-list">
            <div class="movie" v-for="movie in movies" :key="movie.imdbID">
                <router-link :to="'/movie/' + movie.imdbID" class="movie-link">
                    <div class="product-image">
                        <img :src="movie.Poster" alt="Movie Poster"/>
                        <div class="type">
                            {{ movie.Type }}
                        </div>
                    </div>
                    <div class="detail">
                        <p class="y">{{ movie.Year}}</p>
                        <h3>{{movie.Title}}</h3>
                    </div>
                </router-link>
            </div>
        </div>
    </div>
</template>

<script>
   import {ref} from 'vue'
   import env from '../env'


   export default {
      setup() {
         const search = ref('');
         const movies = ref([]);

         const SearchMovies = () => {
            if (search.value != "") {
               fetch(`https://www.omdbapi.com/?apikey=${env.apikey}&s=${search.value}`)
                  .then(response => response.json())
                  .then(data => {
                     movies.value = data.Search;
                     search.value = "";
                  })
            }
         }

         return {
            search,
            movies,
            SearchMovies
         }
      }
   }
</script>

<style lang="scss">
    @media only screen and (max-width: 600px) {
        .home {
            width: 100%!important;
            position: absolute;
            left: 50%;
            transform: translate(-50%, 0);

            .movies-list {
                display: flex;
                flex-wrap: wrap;
                margin: 0px 8px;


                .movie {
                    max-width: 50%;
                    flex: 1 1 50%!important;
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
                                background-color: #42b883;
                                color: white;
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

                            .y {
                                color: #AAA;
                                font-size: 14px;
                            }

                            h3 {
                                color: white;
                                font-weight: 600;
                                font-size: 18px;
                            }


                        }
                    }
                }
            }
        }

    }

    .home {
        width: 50%;
        position: absolute;
        left: 50%;
        transform: translate(-50%, 0);

        .feature-card {
            position: relative;

            .featured-img {
                display: block;
                width: 100%;
                height: 300px;
                object-fit: cover;

                position: relative;
                z-index: 0;
            }

            .detail {
                position: absolute;
                left: 0;
                right: 0;
                bottom: 0;
                background-color: rgba(0, 0, 0, 0.6);
                padding: 16px;
                z-index: 1;
            }

            h3 {
                color: white;
                margin-bottom: 16px;
            }

            p {
                color: white;
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
                appearance: none;
                border: none;
                outline: none;
                background: none;

                &[type='text'] {
                    width: 100%;
                    color: white;
                    background: #496583;
                    font-size: 20px;
                    padding: 10px 16px;
                    border-radius: 8px;
                    margin-bottom: 15px;
                    transition: 0.4s;

                    &::placeholder {
                        color: #f3f3f3
                    }

                    &:focus {
                        box-shadow: 0px 3px 6px rgba(0, 0, 0, 0.2);
                    }
                }

                &[type="submit"] {
                    width: 100%;
                    max-width: 300px;
                    background-color: #42b883;
                    padding: 16px;
                    border-radius: 8px;
                    color: white;
                    font-size: 20px;
                    text-transform: uppercase;
                    transition: 0.4s;

                    &:active {
                        background-color: #3b8078;
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
                flex: 1 1 25%;
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
                            background-color: #42b883;
                            color: white;
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

                        .y {
                            color: #AAA;
                            font-size: 14px;
                        }

                        h3 {
                            color: white;
                            font-weight: 600;
                            font-size: 18px;
                        }


                    }
                }
            }
        }
    }
</style>
