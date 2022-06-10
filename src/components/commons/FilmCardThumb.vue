<template>
    <img :src="`https://image.tmdb.org/t/p/w342${film.poster_path}`" alt="">
</template>

<script>
export default {
    name: 'FilmCardThumb',
    props: {
        film: Object,
        Tv: Object,
    }
}
</script>

<style scoped lang="scss">
</style>