<template lang="pug">
  section.hero.is-success
    .hero-head
      header.nav
        .container
          .nav-left
            .nav-item
              strong platziMusic
          .nav-right.nav-menu
            router-link.nav-item(to="/") Buscar
            router-link.nav-item(:to="{name: 'about'}") Nosotros
    .hero-body
      .container.has-text-centered
        h1.title platziMusic
        h1.subtitle Canciones que estan sonando ahora
        pm-player
        
</template>
<script>
import PmPlayer from '@/components/player.vue'
export default {
  components: {
    PmPlayer
  }
}
</script>