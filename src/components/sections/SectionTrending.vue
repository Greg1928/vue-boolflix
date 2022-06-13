<template>
  <section>
    <h1>Serie TV in tendenza</h1>
    <ol>
      <li v-for="(trend, index) in trendingTv" :key="trend.i" @mouseover="mouseover(index)" @mouseleave="mouseleave(index)">
        <img :src="`https://image.tmdb.org/t/p/w342${trend.poster_path}`" alt="">
        <div class="over" :class="{block : trend.media_type === 'tvs'}"> 
          <div class="content">
            <p><span>Titolo: </span> {{trend.name}}</p>
            <p><span>Titolo Originale: </span>{{trend.original_name}}</p>
            <p>Voto: <span v-for="n in votesTv[index]" :key="n"><i class="fa-solid fa-star"></i></span></p>
            <p><span>Overview: </span>{{trend.overview}}</p>
          </div>
        </div>
      </li>
    </ol>
    <h1>Film in tendenza</h1>
    <ol>
      <li v-for="(trend, index) in trendingMv" :key="trend.i"  @mouseover="mouseoverMv(index)" @mouseleave="mouseleaveMv(index)">
        <img :src="`https://image.tmdb.org/t/p/w342${trend.poster_path}`" alt="">
        <div class="over" :class="{block : trend.video === 'movies'}"> 
          <div class="content">
            <p><span>Titolo: </span>{{trend.title}}</p>
            <p><span>Titolo Originale: </span>{{trend.original_title}}</p>
            <p>Voto: <span v-for="n in votesMv[index]" :key="n"><i class="fa-solid fa-star"></i></span></p>
            <p><span>Overview: </span>{{trend.overview}}</p>
          </div>
        </div>
      </li>
    </ol>
  </section>
</template>

<script>
import axios from 'axios'

export default {
    name: 'SectionTrending',
    data(){
        return{
            trendingTv: [],
            trendingMv: [],
            votesTv: [],
            votesMv: []
        }
      },
      created(){
        axios.get('https://api.themoviedb.org/3/trending/all/week', {
          params:{
            api_key: '8c5b607d815956781cffe0cfa80918d4',
          }
        }).then((response) => {
          for (let i = 0; i < response.data.results.length; i++) {
            if(response.data.results[i].media_type === 'tv'){
            this.trendingTv.push(response.data.results[i]);
            this.votesTv.push(Math.ceil(response.data.results[i].vote_average / 2));
          }else if(response.data.results[i].media_type === 'movie'){
            this.trendingMv.push(response.data.results[i]);
            this.votesMv.push(Math.ceil(response.data.results[i].vote_average / 2));
          }
          }
        }).catch((err) => {
            console.log(err);
        });
    },
    methods: {
    mouseover: function(index){
      this.trendingTv[index].media_type = 'tvs';
    }, 
    mouseleave: function(index){
      this.trendingTv[index].media_type = 'tv';

    },
    mouseoverMv: function(index){
      this.trendingMv[index].video = 'movies';
    }, 
    mouseleaveMv: function(index){
      this.trendingMv[index].video = 'movie';

    },
    
}
}
</script>

<style scoped lang="scss">
section{
  display: none;

  h1{
    font-size: 30px;
    text-transform: uppercase;
    margin: 20px 20px;
    color: white;
  }

  ol{
    display: flex;
    list-style: none;
    overflow-x: auto;
    background-color: black;
    padding-left: 20px;
  }
  li{
    margin: 2rem .5rem;
    cursor: pointer;
    position: relative;
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
    text-align: center;
    overflow-y: auto;


    .content{
      padding: 40px 20px;

      span{
        font-weight: bold;
      }
      .fa-star{
        color: gold;
      }
    }
  }
  img{
    border: 1px solid white;  
  }
  .block{
    opacity: 1;
  }
}
</style>