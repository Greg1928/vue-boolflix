<template>
  <section>
    <input type="text" placeholder="  Cerca film o serie Tv" @keyup.enter="filterTv(), filterFilms()" v-model="dataShared.InputText">
    <button @click="filterTv(), filterFilms()"><i class="fa-solid fa-magnifying-glass"></i></button>
    <div :class="{none : dataShared.InputText === ''}" >
      <h1>I tuoi risultati nella categoria Film</h1>

      <div class="list">
        <div class="thumb" v-for="(film, index) in films" :key="film.id" @mouseover="mouseoverMv(index), voteMv(index)" @mouseleave="mouseleaveMv(index)">
          <FilmCardThumb :film="film"/>
          <div class="over" :class="{show : film.video === 'true'}"> 
            <div class="content">
              <p><span>Titolo: </span> {{film.title}}</p>
              <p><span>Titolo Originale: </span>{{film.original_title}}</p>
              <p>Voto: <span v-for="n in votes" :key="n"><i class="fa-solid fa-star"></i></span></p>
              <p><span>Overview: </span>{{film.overview}}</p>
            </div>
          </div>
        </div>
      </div>
        <h1>I tuoi risultati nella categoria Serie Tv</h1>
      <div class="list">
        <div class="thumb" v-for="(serie,index) in Tv" :key="serie.id" @mouseover="mouseoverTv(index), voteTv(index)" @mouseleave="mouseleaveTv(index)">
          <TvCardThumb :Tv="serie"/>
          <div class="over" :class="{show : serie.vote_count === 'true'}"> 
              <div class="content">
                <p><span>Titolo: </span> {{serie.name}}</p>
                <p><span>Titolo Originale: </span>{{serie.original_name}}</p>
                <p>Voto: <span v-for="n in votes" :key="n"><i class="fa-solid fa-star"></i></span></p>
                <p><span>Overview: </span>{{serie.overview}}</p>
              </div>
          </div>
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
            dataShared,
            votes: 0
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
            console.log(this.films);
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
    mouseoverTv: function(index){
      this.Tv[index].vote_count = 'true';
    }, 
    mouseleaveTv: function(index){
      this.Tv[index].vote_count = 'false';

    },
    mouseoverMv: function(index){
      this.films[index].video = 'true';
    }, 
    mouseleaveMv: function(index){
      this.films[index].video = 'false';

    }, 
     voteTv(index){
          let n = (Math.ceil(this.Tv[index].vote_average / 2));
            this.votes = n;
          },
        
            
        voteMv(index){
            let n = (Math.ceil(this.films[index].vote_average / 2));
            this.votes = n;
            }
},
}
</script>

<styles scoped lang="scss">
section{
   text-align: right;
  h1{
    color: white;
    text-align: center;
    margin-top: 20px;
  }
  input{
    width: 300px;
    border: solid 3px black;
  }
  button{
      width: 70px;
      background-color: black;
      margin-right: 20px;
      border: solid 1px red;
      border-radius: 3px;
      path{
        color: white;
      }
    }

  .list{
  overflow-x: auto;
  overflow-y: hidden;
  display: flex;
  background-color: black;

    .thumb{
        cursor: pointer;
        position: relative;
        margin: 2rem;

        .show{
          opacity: 1;
          }
      }

        .over{
        position: absolute;
        top: 0;
        left: 0;
        bottom: 0;
        z-index: 1;
        color: white;
        background-color: rgba($color: #000000, $alpha: 0.8);
        max-width: 100%;
        opacity: 0;
        transition: opacity 0.2s;
        text-align: left;

        .content{
          margin: 40px 0 0 10px;

          span{
            font-weight: bold;
          }

          .fa-star{
              color: gold;
      }
        }
    }
    }
    .none{
      display: none;
    }
    
  
}


</styles>