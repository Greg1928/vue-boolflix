<template>
  <main>
    <input type="text" @keyup.enter="filterFilms()" v-model="InputText">
    <button @click="filterFilms()">Search</button>
    <ol>
      <li v-for="(film, i) in films" :key="film.id">
        <h1>Titolo: {{film.title}}</h1>
        <h2>Titolo Originale: {{film.original_title}}</h2>
        <h3>Lingua: <img :src="dynamicFlags(i)"/></h3>
        <h4>Voto: {{film.vote_average}}</h4>
        <hr>
      </li>
    </ol>
  </main>
</template>

<script>
import axios from 'axios'
import imageIt from '../../assets/img/220px-Flag_of_Italy_(Pantone,_2003–2006).svg.png'
import imageGb from '../../assets/img/Eng.png'
import imageEs from '../../assets/img/Flag_of_Spain.svg.png'
import imageFr from '../../assets/img/Flag_of_France.png'
import imageRest from '../../assets/img/mundo-comunicacion-red_42634-20.webp.png'

export default {
  name: 'BaseMain',
   data(){
        return{
            films: [],
            InputText: '',
        }
    },
    methods:{
      filterFilms(){
        axios.get('https://api.themoviedb.org/3/search/movie', {
            params:{
                api_key: '8c5b607d815956781cffe0cfa80918d4',
                query: this.InputText,
                // language: 'it-IT'
            }
        }).then((response) =>{
            this.films = response.data.results
        }).catch((err) => {
            console.log(err);
        })
      },
    dynamicFlags(i){
      if(this.films[i].original_language === 'it'){
        return imageIt
      }else if(this.films[i].original_language === 'en'){
        return imageGb
      }else if(this.films[i].original_language === 'es'){
        return imageEs
    }else if(this.films[i].original_language === 'fr'){
        return imageFr
    }else{
      return imageRest
    }
    }
}
}
</script>


<style scoped lang="scss">
img{
  max-width: 30px;
  vertical-align: middle;
}
</style>
