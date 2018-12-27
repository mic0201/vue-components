<template lang="pug">
  #Home.main-section.grid
    .media-card-container
      h2 Media Card
      MediaCard
    .bar-with-tag-container
      h2 Bar With Tag
      BarWithTag(:setting="barWithTagProps" :delay="1000" :duration="5000")
</template>

<script>
import MediaCard from '@/components/MediaCard.vue'
import BarWithTag from '@/components/BarWithTag.vue'

// Props
import barWithTagProps from '../components/props/barWithTagProps.json'

export default {
  name: 'home',
  components: {
    MediaCard,
    BarWithTag
  },
  data: function () {
    return {
      barWithTagProps: {}
    }
  },
  mounted() {
    this.barWithTagProps = barWithTagProps
  }
}
</script>

<style lang="sass" scoped>

  .main-section
    h2
      margin: 0

</style>
