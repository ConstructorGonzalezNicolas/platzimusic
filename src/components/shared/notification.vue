<template lang="pug">
  .container
    .columns
      .column.is-5.is-offset-4
        .notification(:class="[importColor]")
          slot(name="body") algo anda mal
          slot(name="mal") esta andando bien
</template>
<script>
export default {
  props: {
    importColor: {type: Object, required: true}
  }
}
</script>
<style lang="scss">
  .notification {
        margin: 10px;
  }    
</style>