<template lang="pug">
  #app
    pm-header
    
    router-view
    
    pm-footer         
</template>

<script>
import PmFooter from '@/components/layout/footer.vue'
import PmHeader from '@/components/layout/header.vue'

export default {
  name: 'app',
  components: {
    PmFooter,
    PmHeader
  }
}
</script>

<style lang="scss">
  @import './scss/main.scss';  
</style>
