<template>
  <main>
    <SectionThumb/>
    <SectionTrending :class="{show : dataShared.InputText === ''}"/>
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
  background-color: var(--primary-color);
  height: calc(100vh - 80px);
  overflow-y: auto;
  .show{
    display: block;
  }
  .none{
    display: none;
  }
}
</style>
