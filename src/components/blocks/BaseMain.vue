<template>
  <main>
    <input type="text" v-model="InputText">
    <button @click="filterFilms()">Search</button>
    <ol>
      <li v-for="film in films" :key="film.id">
        <h1>Titolo: {{film.title}}</h1>
        <h2>Titolo Originale: {{film.original_title}}</h2>
        <h3>Lingua: {{film.original_language}}</h3>
        <h4>Popolarità: {{film.popularity}}</h4>
        <hr>
      </li>
    </ol>
  </main>
</template>

<script>
import axios from 'axios'

export default {
  name: 'BaseMain',
   data(){
        return{
            films: [],
            InputText: ''
        }
    },
    methods:{
      filterFilms(){
        axios.get('https://api.themoviedb.org/3/search/movie', {
            params:{
                api_key: '8c5b607d815956781cffe0cfa80918d4',
                query: this.InputText,
                language: 'it-IT'
            }
        }).then((response) =>{
            this.films = response.data.results
        }).catch((err) => {
            console.log(err);
        })
      }
    }
}
</script>


<style scoped lang="scss">

</style>
