<template lang="pug">
  main
    transition(name="move") 
      pm-notification(v-show="showNotification", v-bind:importColor="{'is-success' :noOsiElement, 'is-danger' :!noOsiElement }")
        p(slot="body", v-show="dangerOrAccess") no se han encontrado Elementos 
        p(slot="mal", v-show="!dangerOrAccess") Se han encontrado {{ this.tracks.length }} elementos

    transition(name="move")  
      pm-loader(v-show="isLoading")

    section.section(v-show="!isLoading")
      nav.nav
        .container
          input.input.is-large(
            type="text",
            placeholder="Buscar canciones",
            v-model="searchQuery"
          )
          a.button.is-info.is-large(@click="search") Buscar
          a.button.is-danger.is-large &times;
      .container      
        p
          small {{ searchMessage }}

      .container.results
        .columns.is-multiline
          .column.is-one-quarter(v-for="t in tracks")
            pm-track(
              v-blur="t.preview_url"
              :class="{'is-active': t.id === selectedTrack }", 
              :track="t", 
              @select="setSelectedTrack"
            )     
</template>

<script>
import trackService from '@/services/track'
import PmTrack from '@/components/track.vue'
import PmLoader from '@/components/shared/loader.vue'
import PmNotification from '@/components/shared/notification.vue'

export default {
  name: 'app',

  data () {
    return {
      searchQuery: '',
      tracks: [],
      isLoading: false,
      selectedTrack: '',
      showNotification: false,
      dangerOrAccess: false,
      noOsiElement: 0
    }
  },

  computed: {
    searchMessage () {
      return `Encontrados: ${this.tracks.length}`
    }
  },
  watch: {
    showNotification () {
      if (this.showNotification) {
        if (this.tracks.length === 0) {
          setTimeout(() => {
            this.showNotification = false
            this.dangerOrAccess = false
          }, 2000)
        }
        if (this.tracks.length > 0) {
          setTimeout(() => {
            this.showNotification = false
            this.dangerOrAccess = true
          }, 2000)
        }
      }
    }
  },
  methods: {
    search () {
      if (!this.searchQuery) { return }
      this.isLoading = true
      trackService.search(this.searchQuery)
        .then(res => {
          this.showNotification = res.tracks.total > 0 || res.tracks.total === 0
          this.noOsiElement = res.tracks.total
          this.tracks = res.tracks.items
          this.isLoading = false
        })
    },
    setSelectedTrack (id) {
      this.selectedTrack = id
    }
  },
  components: {
    PmTrack,
    PmLoader,
    PmNotification
  }
}
</script>

<style lang="scss">
  .results {
    margin-top: 50px;
  }
    .is-active {
      border: 3px #23d160 solid;    
    }  
</style>
