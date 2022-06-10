<template>
     <img :src="`https://image.tmdb.org/t/p/w342${Tv.poster_path}`" alt="">
</template>

<script>
export default {
    name: 'TvCardThumb',
    props: {
        film: Object,
        Tv: Object,
    }
}
</script>

<style scoped lang="scss">
img{
    border: 1px solid white;
}
</style>