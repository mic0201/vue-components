<template lang="pug">
  a.mediaCard(:href="data.link" target="_blank")
    .header.flex
      img(:src="data.logo")
      h4 {{ data.title }}
    .body
      p {{ data.description }}
    .time {{ data.date }}
    .back
      p {{ data.back }}
</template>

<script>
export default {
  name: "MediaCard",
  props: {
    data: {
      type: Object,
      default: {
        logo: "/img/news/storm.svg",
        title: "金正恩、文在寅簽署《平壤共同宣言》：兩韓打造和平朝鮮半島，共同申辦2032年奧運！",
        description: "在北韓（朝鮮）進行訪問的南韓總統文在寅，19日與朝鮮國務委員會委員長金正恩19日在百花園國賓館進行「平壤峰會」第二場會談",
        link: "https://udn.com/news/story/6656/3557151",
        date: "2018-12-31 15:30",
        back: "背面訊息背面訊息背面訊息背面訊息背面訊息背面訊息背面訊息背面訊息背面訊息背面訊息背面訊息背面訊息背面訊息背面訊息背面訊息背面訊息背面訊息背面訊息背面訊息背面訊息背面訊息"
      }
    }
  },
  data: function () {
    return {
    }
  }
}
</script>

<style lang="sass" scoped>
  @import '../sass/mixin.sass'

  $cardW: 500px
  $cardH: 180px

  .mediaCard
    display: inline-block
    position: relative
    width: calc(100% / 2 - 30px)
    +rwd-max900px
      width: 100%
    max-width: $cardW
    max-height: $cardH
    padding: 3px 15px
    margin-top: 30px
    overflow: hidden
    &:hover
      .back
        transform: translateY(0)
    .header
      align-items: center
      img
        width: 120px
      h4
        margin-left: 15px
    .time
      text-align: right
    .back
      position: absolute
      left: 0
      bottom: 0
      width: 100%
      height: 60px
      transform: translateY(120px)
      background-color: rgba(0,0,0,0.6)
      transition: transform .3s
      > p
        color: white
        margin: 0 1rem
</style>
