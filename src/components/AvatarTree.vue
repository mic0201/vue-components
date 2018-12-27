<template lang="pug">
  .Avatar-tree
    .avatar
      template(v-for="(avatar, index) in setting")
        //- 排版用元素
        template(v-if="index === 0 || (index === setting.length -1 && (setting.length - 4) % 5 === 0)")
          .imgbox.container
        //- MAIN
        Avatar(:index="index" :reverse="false" :avatar="avatar.img" :category="avatar.category" @selected="selected")
        //- 排版用元素
        template(v-if="index === 0 || (index === setting.length -1 && ((setting.length - 4) % 5 === 0 || (setting.length - 2) % 5 === 0 || setting.length % 5 === 0))")
          .imgbox.container

</template>

<script>
import Avatar from '@/components/Avatar'

export default {
  name: "AvatarTree",
  components: {
    Avatar
  },
  props: {
    setting: {
      type: Array,
      default: function () {
        return []
      }
    }
  },
  data: function () {
    return {}
  },
  methods: {
    selected(index) {
      this.$emit('selected', index)
    }
  },
  /**
   * [First] [Last] Element
   * have to add two fack element
   * 4, 9, 14, 19 ..... => arr.length - 4 % 5 === 0
   * have to add two fack element
   * 2, 7 ,12 .... => arr.length - 2 % 5 === 0
   * have to add the fack element in the end
   * 5, 10, 15 ... => arr.length % 5 === 0
   * have to add the fack element in the end
   */
  detectTheEmptyEle(state, index) {
    switch (state) {
      case 'front':
        if (index === 0 || (index === team.avatars.length - 1 && (team.avatars.length - 4) % 5 === 0)) {
          return true
        }
      case 'back':
        if (index === 0 || (index === team.avatars.length - 1 && ((team.avatars.length - 4) % 5 === 0 || (team.avatars.length - 2) % 5 === 0 || team.avatars.length % 5 === 0))) {
          return true
        }
    }

  }
}
</script>

<style lang="sass" scoped>


  .Avatar-tree
    display: flex
    zoom: 0.9
    @media screen and (max-width: 740px)
      flex-direction: column
    @media screen and (max-width: 420px)
      zoom: 0.8

    .avatar
      display: flex
      justify-content: center
      align-items: center
      flex-wrap: wrap
      width: 480px
      @media screen and (max-width: 1019px)
        zoom: 0.8
      @media screen and (max-width: 740px)
        margin: auto
      .imgbox
        width: 150px
        height: 200px
        overflow: hidden
        &.container
          transform: rotate(120deg)
          visibility: hidden
          margin: 0px 5px
          &:nth-of-type(n+4)
            margin-top: -60px
          &:nth-of-type(5n+4)
            margin-left: 8px

</style>
