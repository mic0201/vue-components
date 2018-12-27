<template lang="pug">
  .avatar-info
    section#member
      .header.flex
        Avatar(:reverse="false" :avatar="setting.img" :category="setting.category")
        h2 
          span {{ setting.name }}
          .small {{ setting.category }}
          .small {{ setting.title }}
      .body
        p {{ setting.info }}
        ul( v-for="(header, index) in setting.list_header" :key="index")
          h3 {{ header === 'general' ? '' : header }}
          li(v-for="(list, index) in setting.list[header]" :key="index") {{ list }}
</template>

<script>
import Avatar from '@/components/Avatar'

export default {
  name: "AvatarInfo",
  components: {
    Avatar
  },
  props: {
    setting: {
      type: Object,
      default: function () {
        return {}
      }
    }
  },
  data: function () {
    return {}
  },
  watch: {
    setting: {
      handler: function (newVal, oldVal) {
        console.log(newVal, oldVal)
      }
    }
  },
  methods: {}
}
</script>

<style lang="sass" scoped>

  .avatar-info
    width: 100%
    min-height: 200px
    @media screen and (max-width: 1019px) and (min-width: 741px)
      width: calc(100% - 570px * 0.7)
    @media screen and (max-width: 740px)
      width: 100%
    padding: 25px
    .header
      &.flex
        align-items: center
        h2
          font-size: 1.8rem
          margin-left: 2rem
          .small
            font-size: 1rem
    .body
      p
        padding-left: 20px
    ul
      li
        &:not(:first-child)
          margin-top: .4rem

</style>
