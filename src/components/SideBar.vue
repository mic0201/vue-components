<template lang="pug">
  .SideBar.flex.column
    .logo-box.flex
      img(src="../assets/logo.png")
    .menu-box.flex.column
      .menu-item(v-for="(item, itemIndex) in menu" @click="clickMenu(itemIndex)")
        i(:class="item.icon")
        a.hoverLeftInRightOut(v-if="item.type === 'page'" :href="item.link") {{ item.name }}
        router-link.hoverLeftInRightOut(v-else-if="item.type === 'component'" :to="item.link") {{ item.name }}
        a.hoverLeftInRightOut(v-else) {{ item.name }}

</template>

<script>
export default {
  name: "SideBar",
  props: {},
  data: function () {
    return {
      activeMenu: {},
      menu: [
        {
          icon: "fas fa-home",
          name: "首頁 / Dashboard",
          type: "component",
          link: "/"
        },
        {
          icon: "fas fa-layer-group",
          name: "帳戶 / Account",
          type: "component",
          link: "/"
        },
        {
          icon: "far fa-user",
          name: "會員 / Membership",
          type: "component",
          link: "/"
        },
        {
          icon: "far fa-credit-card",
          name: "理財 / Finance",
          type: "component",
          link: "/"
        },
        {
          icon: "fas fa-sign-out-alt",
          name: "登出 / Logout",
          type: "function",
          link: "/"
        }
      ]
    }
  },
  methods: {
    clickMenu(itemIndex) {
      this.activeMenu = this.menu[itemIndex]
    }
  }
}
</script>

<style lang="sass" scoped>
  @import '../sass/setting.sass'

  .SideBar
    width: 100%
    height: 100%
    background-color: $keyColor_1
    padding: 1rem 0
    box-sizing: border-box
    &.flex
      align-items: center

    .logo-box
      width: 50%
      &.flex
        align-items: center

    .menu-box
      height: 70%
      &.flex
        justify-content: center
      i
        margin-right: .7rem
      .menu-item
        color: $keyColor_5
        opacity: 1
        &:not(:first-child)
          margin-top: 1rem
        &.active
          color: $keyColor_3

</style>
