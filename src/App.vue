<template>
  <div id="app">
    <BaseHeader/>
    <BaseMain/>
  </div>
</template>

<script>
import BaseHeader from './components/blocks/BaseHeader.vue'
import BaseMain from './components/blocks/BaseMain.vue'

export default {
  name: 'App',
  components: {
    BaseMain,
    BaseHeader
  }
}
</script>

<style lang="scss">
@import './assets/style/global.scss';
</style>
