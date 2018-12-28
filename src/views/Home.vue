<template lang="pug">
  #Home.main-section.grid
    .media-card-container
      h2 Media Card
      MediaCard
    .bar-with-tag-container
      h2 Bar With Tag
      BarWithTag(:setting="barWithTagProps" :delay="1000" :duration="5000")
    .roadmap-container
      h2 Roadmap
      Roadmap(:setting="roadmapProps")
    .avatar-container
      h2 Avatar
      Avatar(:avatar="avatarProps.img")
    .avatar-tree-container
      h2 Avatar Tree
      AvatarTree(:setting="avatarTreeProps" @selected="avatarTreeSelectInfo")
    .avatar-info-container
      h2 Avatar Info
      AvatarInfo(:setting="avatarInfoProps")
    .tabs-container
      h2 Tabs
      Tabs(:tabs="tabsProps" @selected="tabsSelectInfo")
    .menu-container
      h2 Menu
      Menu(:menu="menuProps")
</template>

<script>
import MediaCard from '@/components/MediaCard'
import BarWithTag from '@/components/BarWithTag'
import Roadmap from '@/components/Roadmap'
import Avatar from '@/components/Avatar'
import AvatarTree from '@/components/AvatarTree'
import AvatarInfo from '@/components/AvatarInfo'
import Tabs from '@/components/Tabs'
import Menu from '@/components/Menu'

// Props
import barWithTagProps from '@/components/props/barWithTagProps.json'
import roadmapProps from '@/components/props/roadmapProps.json'
import avatarProps from '@/components/props/avatarProps.json'
import avatarTreeProps from '@/components/props/avatarTreeProps.json'
import avatarInfoProps from '@/components/props/avatarInfoProps.json'
import tabsProps from '@/components/props/tabsProps.json'
import menuProps from '@/components/props/menuProps.json'

export default {
  name: 'home',
  components: {
    MediaCard,
    BarWithTag,
    Roadmap,
    Avatar,
    AvatarTree,
    AvatarInfo,
    Tabs,
    Menu
  },
  data: function () {
    return {
      barWithTagProps: {},
      roadmapProps: [],
      avatarProps: {},
      avatarTreeProps: [],
      avatarInfoProps: {},
      tabsProps: [],
      menuProps: {}
    }
  },
  mounted() {
    this.barWithTagProps = barWithTagProps
    this.roadmapProps = roadmapProps
    this.avatarProps = avatarProps
    this.avatarTreeProps = avatarTreeProps
    this.avatarInfoProps = avatarInfoProps
    this.tabsProps = tabsProps
    this.menuProps = menuProps
  },
  methods: {
    avatarTreeSelectInfo(index) {
      console.log('select', index)
    },
    tabsSelectInfo(index) {
      console.log('select', index)
    }
  }
}
</script>

<style lang="sass" scoped>

  .main-section
    h2
      margin: 0

  .menu-container
    height: 60px

</style>
