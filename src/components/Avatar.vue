<template lang="pug">
  .imgbox.container(:class="[custom_class, transpose]" @click="selected(index)")
    .imgbox.wrapper
      .imgbox.main(:style="{ backgroundImage: `url(${avatar})` }")
</template>

<script>
export default {
  name: "Avatar",
  props: {
    index: Number,
    avatar: String,
    category: String,
    reverse: Boolean
  },
  data: function() {
    return {
      custom_class: this.$props.category,
      transpose: this.$props.reverse ? "transpose" : ""
    }
  },
  methods: {
    selected: function selected(index) {
      this.$emit("selected", index)
    }
  }
}
</script>

<style lang="sass" scoped>
  @import '@/sass/setting.sass'
  $imgW: 150px
  $imgH: 200px

  @mixin size
    width: $imgW
    height: $imgH

  @mixin publicSetting($rotate, $visible)
    transform: rotate($rotate)
    visibility: $visible
    background-size: cover
    background-position: 50% 50%

  .imgbox
    +size
    overflow: hidden
    &.container.hide
      +disappear
      @media screen and (max-width: 1080px)
        display: none
    &.container
      +publicSetting(120deg, hidden)
      margin: 0px 5px
      &.transpose
        +publicSetting(-60deg, hidden)
      > .wrapper
        +publicSetting(-60deg, hidden)
        > .main
          +publicSetting(-60deg, visible)

</style>
