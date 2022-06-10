<template>
  <section>
        <input type="text" placeholder="Cerca film o serie Tv" v-model="dataShared.InputText">
        <button @click="filterTv(), filterFilms()">Search</button>
        <div :class="{none : dataShared.InputText === ''}">
            <h1>I tuoi risultati nella categoria Film</h1>

            <div class="list">
                <div class="thumb">
                    <FilmCardThumb v-for="(film) in films" :key="film.id" :film="film"/>
                </div>
            </div>
            <h1>I tuoi risultati nella categoria Serie Tv</h1>
            <div class="list">
                <div class="thumb">
                    <TvCardThumb v-for="(serie) in Tv" :key="serie.id" :Tv="serie"/>
                </div>
            </div>
        </div>
    </section>
</template>

<script>
import axios from 'axios'
import imageIt from '../../assets/img/220px-Flag_of_Italy_(Pantone,_2003–2006).svg.png'
import imageGb from '../../assets/img/Eng.png'
import imageEs from '../../assets/img/Flag_of_Spain.svg.png'
import imageFr from '../../assets/img/Flag_of_France.png'
import imageRest from '../../assets/img/mundo-comunicacion-red_42634-20.webp.png'
import FilmCardThumb from '../commons/FilmCardThumb.vue'
import TvCardThumb from '../commons/TvCardThumb.vue'
import dataShared from '../../shared/dataShared'

export default {
    name: 'SectionThumb',
    components: {FilmCardThumb, TvCardThumb},
    data(){
        return{
            films: [],
            Tv: [],
            dataShared
        }
    },
    methods:{
      filterFilms(){
        axios.get('https://api.themoviedb.org/3/search/movie', {
            params:{
                api_key: '8c5b607d815956781cffe0cfa80918d4',
                query: this.dataShared.InputText,
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
                query: this.dataShared.InputText,
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

<styles scoped lang="scss">
section{
  // display: none;

  .list{
  overflow-x: auto;

    .thumb{
        display: flex;
    }
    
}
.none{
  display: none;
}
}

</styles>