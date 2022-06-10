<template>
  <section>
    <div class="container">
      <h1>Serie TV Trends</h1>
    <ol>
      <li v-for="trend in trendingTv" :key="trend.i">
        <img :src="`https://image.tmdb.org/t/p/w342${trend.poster_path}`" alt="">
      </li>
    </ol>
    <h1>Film Trends</h1>
    <ol>
      <li v-for="trend in trendingMv" :key="trend.i">
        <img :src="`https://image.tmdb.org/t/p/w342${trend.poster_path}`" alt="">
      </li>
    </ol>
    </div>
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
          }else if(response.data.results[i].media_type === 'movie'){
            this.trendingMv.push(response.data.results[i]);
          }
          }
          console.log(this.trendingMv);
        }).catch((err) => {
            console.log(err);
        });
    },
}
</script>

<style scoped lang="scss">
section{
  display: none;

  h1{
    text-align: center;
    font-size: 40px;
  }

  ol{
    display: flex;
    justify-content: center;
    list-style: none;
    overflow-x: auto;

  }
  li{
    margin: 10px;
  }
  img{
    border: 1px solid white;  
  }
}
</style>