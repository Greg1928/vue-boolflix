<template>
  <main>
    
    <!-- <SectionTrending :class="{show : InputText === ''}"/> -->
    <!-- <div :class="{none : InputText === ''}"> -->
      <SectionThumb/>
      <SectionTrending :class="{show : dataShared.InputText === ''}"/>
      <!-- <ol>
        <li v-for="(film, i) in films" :key="film.id">
          <h1>Titolo: {{film.title}}</h1>
          <h2>Titolo Originale: {{film.original_title}}</h2>
          <h3>Lingua: <img :src="dynamicFlagsFilm(i)"/></h3>
          <h4>Voto: {{film.vote_average}}</h4>
        </li>
      </ol> -->
    <!-- </div> -->
     <!-- <div :class="{none : InputText === ''}">
      <h1>I tuoi risultati nella categoria TV</h1>
      <ol>
        <li v-for="(tv, i) in Tv" :key="tv.id">
          <h1>Titolo: {{tv.name}}</h1>
          <h2>Titolo Originale: {{tv.original_title}}</h2>
          <h3>Lingua: <img :src="dynamicFlagsTv(i)"/></h3>
          <h4>Voto: {{tv.vote_average}}</h4>
        </li>
      </ol>
    </div> -->
  </main>
</template>

<script>
import dataShared from '@/shared/dataShared'
import SectionTrending from '../sections/SectionTrending.vue'
import SectionThumb from '../sections/SectionThumb.vue'

export default {
  name: 'BaseMain',
  components: { SectionThumb, SectionTrending },
  data(){
    return{
      dataShared
    }
  }
   
}
</script>


<style scoped lang="scss">
main{

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
}
</style>
