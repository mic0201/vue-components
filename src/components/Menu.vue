<template lang="pug">
  .menu.flex
    .item-box(v-for="(item, index) in menu.menu" :key="index")
      router-link.item.flex(v-if="item.type === 'page'" :to="item.link") {{ item.name }}
      a.item.flex(v-else-if="item.type === 'url'" :href="item.link" target="_blank") {{ item.name }}
      a.item.flex(v-else-if="item.type === 'file'" :href="item.link" target="_blank") {{ item.name }}
      a.item.flex(v-else-if="item.type === 'download'" :href="item.link" target="_blank" download="download") {{ item.name }}
      a.item.flex(v-else) {{ item.name }}
        //- Layer 1
        .itemList.disappear.flex(v-if="item.isList")
          router-link.subItem(v-if="!subItem.isList" v-for="(subItem, subIndex) in item.item" :key="subIndex" :to="subItem.link") {{ subItem.name }}
          a.subItem(v-else) {{ subItem.name }}
            .icon-box(v-if="subItem.isList")
              i.fas.fa-chevron-right
            //- Layer 2
            .subItemList.disappear.flex(v-if="subItem.isList")
              router-link.subItem_item(v-for="(subItem_item, subItem_itemIndex) in subItem.item" :key="subItem_itemIndex" :to="subItem_item.link") {{ subItem_item.name }}
    .lang-icon.flex(@click="expandLangList")
      i.fas.fa-globe
      .langList(:class="openLangList")
        .lang(v-for="lang in menu.lang" @click="setLang(lang.lang)")
          span {{ lang.name }}

</template>

<script>
export default {
  name: "Menu",
  props: {
    menu: Object,
  },
  data: function () {
    return {
      lang: 'tw',
      openLangList: "",
    }
  },
  methods: {
    setLang(lang) {
      this.lang = lang
      this.$router.push({ query: { lang: this.lang } })
      this.$emit('setLang', this.lang)
    },
    expandLangList() {
      this.openLangList = this.openLangList === 'open' ? '' : 'open'
    }
  }
}
</script>

<style lang="sass" scoped>
  @import '../sass/setting.sass'

  @mixin show($top)
    top: $top !important
    opacity: 1 !important
    visibility: visible !important
    transition: opacity .5s !important
    transition-delay: .1s !important

  @mixin showTab($top)
    +show($top)

  @mixin showList($top, $left)
    left: $left !important
    +show($top)

  @mixin showListRight($top, $right)
    right: $right !important
    +show($top)

  @mixin whenHoverList
    background-color: $keyColor_4

  @mixin whenHoverItem
    background-color: $keyColor_2

  .menu
    background-color: $keyColor_3
    height: 100%
    font-size: 0.5rem
    &.flex
      align-items: center

    > .item-box
      height: 100%
      > .item
        position: relative
        max-width: 120px
        height: 100%
        color: white
        padding: 0px 15px
        transition: background-color .15s
        &.flex
          align-items: center
          justify-content: center
          flex-direction: column
          
        *
          color: white
          background-color: $keyColor_1

        a
          padding: 10px 12px

        &:hover
          background-color: $keyColor_5
          > .itemList
            z-index: 1 !important
            +showList(100%, 0)

        > .itemList
          min-width: 200px
          flex-direction: column
          &.disappear
            +disappear
          &:hover
            > .subItem
              +whenHoverList
              > .icon-box
                > i
                  color: white

          > .subItem
            position: relative
            &.disappear
              +disappear
            > .icon-box
              position: absolute
              right: 10px
              background-color: transparent
              > i
                font-size: 0.5rem
                opacity: 0.7
                background-color: transparent
            &:hover
              +whenHoverItem
              > .icon-box
                > i
                  color: #3e3939

              > .subItemList
                +showListRight(0, 100%)

            > .subItemList
              min-width: 170px
              &.flex
                flex-direction: column
              &.disappear
                +disappear
              &:hover
                > .subItem_item
                  +whenHoverList

              > .subItem_item
                &:hover
                  +whenHoverItem

    .lang-icon
      position: relative
      color: white
      min-width: 60px
      cursor: pointer
      &.flex
        justify-content: center

      .langList
        min-width: 200px
        z-index: 1
        color: white
        background-color: $keyColor_3
        right: 0
        +disappear
        &.open
          top: 36px
          z-index: 1
          opacity: 1
          visibility: visible

        .lang
          padding: .3rem .6rem
          &:hover
            background-color: $keyColor_5


</style>
