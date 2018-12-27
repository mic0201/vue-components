<template lang="pug">
  section#roadmap.flex
    .body
      .line
        .stone.fas.fa-square(v-for="road in setting")
          .content
            h2.s-title {{ road.date }}
            p.s-description {{ road.description }}
            ul
              li(v-for="(list, index) in road.list" :key="index") {{ list }}
</template>

<script>

export default {
  name: "Roadmap",
  props: {
    setting: {
      type: Array,
      default: function () {
        return []
      }
    }
  },
  watch: {
    roadmap: {
      immediate: true,
      handler: function (newVal, oldVal) {
        setTimeout(() => {
          document.querySelectorAll(".stone:nth-child(odd) .content").forEach(d => this.setStoneHeight(d))
          document.querySelectorAll(".stone .content").forEach(d => this.addNowMonth(d))
        }, 1000)
      }
    }
  },
  methods: {
    dateToMonth(month, fullyear) {
      month = month.toString()
      let res = ''
      switch (month) {
        case '1':
          res = 'January'
          break;
        case '2':
          res = 'February'
          break;
        case '3':
          res = 'March'
          break;
        case '4':
          res = 'April'
          break;
        case '5':
          res = 'May'
          break;
        case '6':
          res = 'June'
          break;
        case '7':
          res = 'July'
          break;
        case '8':
          res = 'August'
          break;
        case '9':
          res = 'September'
          break;
        case '10':
          res = 'October'
          break;
        case '11':
          res = 'November'
          break;
        case '12':
          res = 'December'
          break;
      }
      return `${res} ${fullyear}`
    },
    setStoneHeight(stone) {
      stone.style.top = -stone.offsetHeight - 40 + "px"
      return
    },
    addNowMonth(stone) {
      let nowMonth = new Date().getMonth() + 1,
        nowYear = new Date().getFullYear(),
        str_Mon = this.dateToMonth(nowMonth, nowYear)
      if (stone.childNodes[0].innerText.indexOf(str_Mon) > -1) {
        stone.parentNode.classList.add("nowMonth")
      }
    }
  }
}
</script>

<style lang="sass" scoped>
  @import '../sass/setting.sass'
  $stoneContentW: 300px
  $roadmapH: 800px
  $roadmapC: #13434a

  @keyframes sparkleSquare
    0%
      transform: scale(1.5) rotate(45deg)
    50%
      transform: scale(1) rotate(45deg)
    100%
      transform: scale(1.5) rotate(45deg)

  ul
    padding-left: 20px
    li
      margin-top: .4rem

  #roadmap
    &.flex
      flex-wrap: wrap

  h1.title
    margin-bottom: 0

  .body
    width: 100%
    min-height: $roadmapH
    display: flex
    align-items: center
    overflow: auto
    color: $roadmapC

  .line
    position: relative
    display: flex
    height: 2px
    background-color: $roadmapC
    transform: translateY(-3rem)
    .stone
      position: relative
      flex: 0 0 auto
      width: 250px
      &.nowMonth
        &:before
          animation: sparkleSquare 1.3s linear 0s infinite alternate
      &:before
        position: absolute
        top: calc(50% - 17px / 2)
        left: calc(50% - 21px / 2)
        transform: rotate(45deg)
      &:nth-child(odd)
        &:after
          position: absolute
          content: ''
          top: calc(50% - 65px / 2)
          left: calc(50% - 10px / 2)
          height: 35px
          width: 2px
          background-color: $roadmapC
      &:nth-child(even)
        &:after
          position: absolute
          content: ''
          top: calc(50% - 2px)
          left: calc(50% - 10px / 2)
          height: 35px
          width: 2px
          background-color: $roadmapC
      .content
        width: $stoneContentW
        position: absolute
        top: 25px
        left: 50%
        font-family: 'Fira Sans', sans-serif
        .s-title,
        .s-description
          margin-left: 0
</style>
