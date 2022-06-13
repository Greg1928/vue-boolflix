<template>
  <header>
    <div class="left-part">
      <h1>boolflix</h1>
      <a href="#">Home</a>
      <a href="#">Serie TV</a>
      <a href="#">Film</a>
    </div>
    <div class="right-part">
      <input type="text" placeholder="  Cerca film o serie Tv" @keyup.enter="filterTv(), filterFilms()" v-model="dataShared.InputText">
      <button @click="filterTv(), filterFilms()"><i class="fa-solid fa-magnifying-glass"></i></button>
      <p>UserName</p>
      <i class="fa-solid fa-gift"></i>
      <i class="fa-solid fa-bell"></i>
      <i class="fa-solid fa-circle-user"></i>
      <i class="fa-solid fa-chevron-down chevron"></i>
    </div>
  </header>
</template>

<script>
import axios from 'axios'
import dataShared from '../../shared/dataShared'

export default {
    name: "BaseHeader",
    data(){
        return{
            dataShared,
        }

    },
     methods:{
      filterFilms(){
        axios.get('https://api.themoviedb.org/3/search/movie', {
            params:{
                api_key: '8c5b607d815956781cffe0cfa80918d4',
                query: dataShared.InputText,
            }
        }).then((response) =>{
            dataShared.films = response.data.results;
            for (let i = 0; i < response.data.results.length; i++){
              dataShared.votesFilm.push(Math.ceil(response.data.results[i].vote_average / 2));
             }
        }).catch((err) => {
            console.log(err);
        })
      },
      filterTv(){
        axios.get('https://api.themoviedb.org/3/search/tv', {
            params:{
                api_key: '8c5b607d815956781cffe0cfa80918d4',
                query: dataShared.InputText,
            }
        }).then((response) =>{
            dataShared.Tv = response.data.results
            for (let i = 0; i < response.data.results.length; i++){
              dataShared.votesSerie.push(Math.ceil(response.data.results[i].vote_average / 2));
             }
        }).catch((err) => {
            console.log(err);
        })
      },
     }
}
</script>

<style lang="scss" scoped>
header{
  background-color: black;
  height: 80px;
  display: flex;
  justify-content: space-between;

  .left-part{
    display: flex;

    a{
      align-self: center;
      margin: 0 15px;
      font-size: 22px;
      text-decoration: none;
      color: white;
    }
  }

  .right-part{
    color: white;
    display: flex;
    align-items: center;
    font-size: 25px;
    margin-right: 30px;

    & *{
      padding: 0 14px;
      cursor: pointer;
    }
    p{
      margin: 0;
    }
    input{
      border-radius: 20px;
      cursor: auto;
    }
    button{
      margin-left: 5px;
      border-radius: 20px;
    }
  }

  h1{
  color: red;
  padding: 15px;
  text-transform: uppercase;
  cursor: pointer;
  }
  .chevron{
    font-size: small;
    padding: 0;
  }
}

</style>