<template lang="pug">
  .Board.inlineflex
    .icon.flex
      i(:class="board.icon")
    .info.flex.column
      h3 {{ board.value }}
      h4 {{ board.title }}
</template>

<script>
export default {
  name: "Board",
  props: {
    board: {
      type: Object,
      default: function () {
        return {
          icon: "fas fa-globe",
          title: "BTC 靜態錢包",
          value: "0.0031466"
        }
      }
    }
  },
  data: function () {
    return {}
  },
  methods: {}
}
</script>

<style lang="sass" scoped>
  @import '../sass/setting.sass'

  .Board
    padding: 1rem 0
    margin: 1rem
    background-color: $keyColor_3

    .icon
      padding: 0 1.5rem
      &.flex
        align-items: center
        justify-content: center
      i
        font-size: 2.5rem

    .info
      padding: 0 2rem 0 .5rem
      h3, h4
        margin: 0

</style>
