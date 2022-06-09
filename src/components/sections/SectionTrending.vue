<template>
  <section>
    <h1>Serie TV Trends</h1>
    <ol>
      <li v-for="trend in trendingTv" :key="trend.i">
        <h2>Titolo: {{trend.name}}</h2>
        <h3>Categoria: {{trend.media_type}}</h3>
        <h4>Popolarità: {{trend.popularity}}</h4>
      </li>
    </ol>
    <h1>Film Trends</h1>
    <ol>
      <li v-for="trend in trendingMv" :key="trend.i">
        <h2>Titolo: {{trend.title}}</h2>
        <h3>Categoria: {{trend.media_type}}</h3>
        <h4>Popolarità: {{trend.popularity}}</h4>
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
    flex-wrap: wrap;
    justify-content: center;
    list-style: none;
  
  li{
    width: 20%;
    border: solid 1px black;
    margin: 10px;
    background-color: lightsalmon;
  }
  }
}
</style>