<template lang="pug">
  .tab-container.flex
    .tab.flex
      .pane(v-for="(tab, tabIndex) in tabs" @click="selectPane($event, tabIndex)")
        span.pane-name(:data-panename="tabIndex") {{ tab }}
</template>

<script>
export default {
  name: "Tabs",
  props: {
    tabs: Array
  },
  data: function () {
    return {
      nowTab: "0"
    }
  },
  watch: {
    tabs: {
      handler: function (newVal, oldVal) {
        this.$nextTick(() => {
          this.activePane()
        })
      }
    }
  },
  methods: {
    selectPane(e, index) {
      this.nowTab = index.toString()
      this.activePane()
      this.$emit('selected', index)
    },
    activePane() {
      let paneNameList = document.querySelectorAll('span[data-panename]')
      paneNameList.forEach(d => {
        if (d.getAttribute('data-panename') === this.nowTab) {
          d.classList.add('active')
        } else {
          d.classList.remove('active')
        }
      })
    }
  }
}
</script>

<style lang="sass" scoped>
  @import '../sass/class.sass'
  @import '../sass/setting.sass'

  .tab-container
    > div
      &:nth-child(1)
        width: 15%
      &:nth-child(2)
        width: 85%

    .tab
      &.flex
        flex-direction: column
      .pane
        cursor: pointer
        &:not(:first-child)
          margin-top: 1rem
        span
          position: relative
          &:before
            content: ''
            position: absolute
            bottom: -5px
            right: 0
            width: 0%
            height: 3px
            background-color: $keyColor_1
            transition: width .3s

          &.active
            &:before
              left: 0
              width: 100%

</style>
