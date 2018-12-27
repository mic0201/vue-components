<template lang="pug">
  #Home.main-section
    .media-card-container
      h1 Media Card
      MediaCard
</template>

<script>
import MediaCard from '@/components/MediaCard.vue'

export default {
  name: 'home',
  components: {
    MediaCard
  }
}
</script>

<style lang="sass" scoped>

  .main-section
    h1
      margin: 0

</style>
