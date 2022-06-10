<template>
  <main>
    <input type="text" placeholder="Cerca film o serie Tv" v-model="InputText">
    <button @click="filterTv(), filterFilms()">Search</button>
    <SectionTrending :class="{show : InputText === ''}"/>
    <div :class="{none : InputText === ''}">
      <h1>I tuoi risultati nella categoria Film</h1>
      <ol>
        <li v-for="(film, i) in films" :key="film.id">
          <h1>Titolo: {{film.title}}</h1>
          <h2>Titolo Originale: {{film.original_title}}</h2>
          <h3>Lingua: <img :src="dynamicFlagsFilm(i)"/></h3>
          <h4>Voto: {{film.vote_average}}</h4>
        </li>
      </ol>
    </div>
     <div :class="{none : InputText === ''}">
      <h1>I tuoi risultati nella categoria TV</h1>
      <ol>
        <li v-for="(tv, i) in Tv" :key="tv.id">
          <h1>Titolo: {{tv.name}}</h1>
          <h2>Titolo Originale: {{tv.original_title}}</h2>
          <h3>Lingua: <img :src="dynamicFlagsTv(i)"/></h3>
          <h4>Voto: {{tv.vote_average}}</h4>
        </li>
      </ol>
    </div>
  </main>
</template>

<script>
import axios from 'axios'
import imageIt from '../../assets/img/220px-Flag_of_Italy_(Pantone,_2003–2006).svg.png'
import imageGb from '../../assets/img/Eng.png'
import imageEs from '../../assets/img/Flag_of_Spain.svg.png'
import imageFr from '../../assets/img/Flag_of_France.png'
import imageRest from '../../assets/img/mundo-comunicacion-red_42634-20.webp.png'
import SectionTrending from '../sections/SectionTrending.vue'

export default {
  name: 'BaseMain',
   components: { SectionTrending },
   data(){
        return{
            films: [],
            Tv: [],
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
      filterTv(){
        axios.get('https://api.themoviedb.org/3/search/tv', {
            params:{
                api_key: '8c5b607d815956781cffe0cfa80918d4',
                query: this.InputText,
                // language: 'it-IT'
            }
        }).then((response) =>{
            this.Tv = response.data.results
            console.log(this.Tv);  
        }).catch((err) => {
            console.log(err);
        })
      },
    dynamicFlagsFilm(i){
      if(this.films[i].original_language === 'it' ){
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
    },
    dynamicFlagsTv(i){
      if(this.Tv[i].original_language === 'it' ){
        return imageIt
      }else if(this.Tv[i].original_language === 'en'){
        return imageGb
      }else if(this.Tv[i].original_language === 'es'){
        return imageEs
    }else if(this.Tv[i].original_language === 'fr'){
        return imageFr
    }else{
      return imageRest
    }
    },
}
}
</script>


<style scoped lang="scss">
h1{
  text-align: center;
}
ol{
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  list-style: none;
  
  li{
    border: solid 1px black;
    margin: 10px;
    background-color: lightgreen;
    text-align: center;
    width: 20%;
  }
}
img{
  max-width: 30px;
  vertical-align: middle;
}
.show{
  display: block;
}
.none{
  display: none;
}
</style>
