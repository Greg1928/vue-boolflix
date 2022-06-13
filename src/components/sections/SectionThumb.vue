<template>
  <section>
    <div :class="{none : dataShared.InputText === ''}">

      <h1>I tuoi risultati nella categoria Film</h1>
      <div class="list">
        <div class="thumb" v-for="(film, index) in dataShared.films" :key="film.id" @mouseover="mouseoverMv(index)" @mouseleave="mouseleaveMv(index)">
          <FilmCardThumb :film="film"/>
          <div class="over" :class="{show : film.video === 'true'}"> 
            <div class="content">
              <p><span>Titolo: </span> {{film.title}}</p>
              <p><span>Titolo Originale: </span>{{film.original_title}}</p>
              <p>Voto: <span v-for="n in dataShared.votesFilm[index]" :key="n"><i class="fa-solid fa-star"></i></span></p>
              <p><span>Overview: </span>{{film.overview}}</p>
            </div>
          </div>
        </div>
      </div>

      <h1>I tuoi risultati nella categoria Serie Tv</h1>
      <div class="list">
        <div class="thumb" v-for="(serie,index) in dataShared.Tv" :key="serie.id" @mouseover="mouseoverTv(index)" @mouseleave="mouseleaveTv(index)">
          <TvCardThumb :Tv="serie"/>
          <div class="over" :class="{show : serie.vote_count === 'true'}"> 
              <div class="content">
                <p><span>Titolo: </span> {{serie.name}}</p>
                <p><span>Titolo Originale: </span>{{serie.original_name}}</p>
                <p>Voto: <span v-for="n in dataShared.votesSerie[index]" :key="n"><i class="fa-solid fa-star"></i></span></p>
                <p><span>Overview: </span>{{serie.overview}}</p>
              </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
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
    props: {
        films: Object,
        Tv: Object,
        votesSerie: Object,
        votesFilm: Object
    },
    data(){
        return{
            dataShared,
        }
        
        },
    methods:{
  
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
        dataShared.Tv[index].vote_count = 'true';
      }, 
      mouseleaveTv: function(index){
        dataShared.Tv[index].vote_count = 'false';

      },
      mouseoverMv: function(index){
        dataShared.films[index].video = 'true';
      }, 
      mouseleaveMv: function(index){
        dataShared.films[index].video = 'false';

      }, 
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

  .list{
  overflow-x: auto;
  overflow-y: hidden;
  display: flex;
  background-color: black;

    .thumb{
        cursor: pointer;
        position: relative;
        margin: 2rem 1.8rem;

        .show{
          opacity: 1;
          }
      }

        .over{
        position: absolute;
        top: 0;
        left: 0;
        bottom: 0;
        right: 0;
        z-index: 1;
        color: white;
        background-color: rgba($color: #000000, $alpha: 0.8);
        max-width: 100%;
        opacity: 0;
        transition: opacity 0.5s;
        text-align: left;
        overflow-y: auto;

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