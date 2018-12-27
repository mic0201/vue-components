<template lang="pug">
  #BarWithTag.flex
    .score-box.flex
      .bar-box(v-for="header in data.score_header")
        h5.score-title {{ header.title }}
        .bar-backing(v-if="header.openBar")
          .bar(:style="{ width: data.score[header.title].now }")
            .tip
              span {{ data.score[header.title].now }}
        .bar-content.flex(v-else)
            h5 USD
            span {{ data.score[header.title].now }}
</template>

<script>

export default {
  name: "BarWithTag",
  props: {
    setting: Object,
    // 出現 bar 條後延遲 x 秒讀值
    delay: Number,
    // 計算數字動畫總時間
    duration: Number
  },
  data: function () {
    return {
      data: {
        score_header: [],
        score: {}
      }
    };
  },
  watch: {
    setting: {
      deep: true,
      handler: function (newVal, oldVal) {
        console.log('in BarWithTag Setting', newVal)
        this.data = JSON.parse(JSON.stringify(newVal))
        Object.keys(this.data.score).forEach(d => {
          this.data.score[d].now = 0
        })
        setTimeout(() => {
          Object.keys(this.data.score).forEach(d => {
            this.data.score[d].backup = newVal.score[d].now
            this.countAnimate(this.data.score[d])
          })
        }, this.delay)
      }
    }
  },
  created() {
    this.bindingRequestAnimationFrame()
  },
  methods: {
    bindingRequestAnimationFrame() {
      let requestAnimationFrame = window.requestAnimationFrame || window.mozRequestAnimationFrame ||
        window.webkitRequestAnimationFrame || window.msRequestAnimationFrame;
      window.requestAnimationFrame = requestAnimationFrame;
    },
    substrNum(str) {
      if (str.toString().indexOf('.') < 0) {
        return str
      }
      str = str.toString()
      let afterDecimalPoint = str.split('.')[1]
      return str = str.replace(afterDecimalPoint, afterDecimalPoint.substr(0, 2))
    },
    // Robert Penner's easeOutExpo
    // c => endNumber d=> duration
    easeOutExpo(t, b, c, d) {
      return c * (-Math.pow(2, -10 * t / d) + 1) * 1024 / 1023 + b;
    },
    countAnimate(score) {
      let start = 0,
        end = score.backup,
        max = score.max,
        self = this

      function callback(timestamp) {
        let val = self.createVal(timestamp, start, end, callback)
        if (score.percentage) {
          score.now = self.substrNum(val / max * 100) + '%'
        } else {
          score.now = val
        }
      }
      requestAnimationFrame(callback.bind(this))
    },
    createVal(timestamp, startVal, endVal, callback) {
      if (!this.startTime) { this.startTime = timestamp }
      this.timestamp = timestamp
      let progress = timestamp - this.startTime;

      let countdown = (startVal > endVal)
      let val = 0
      if (countdown) {
        val = startVal - this.easeOutExpo(progress, 0, startVal - endVal, this.duration);
        val = val < endVal ? endVal : val
      } else {
        val = this.easeOutExpo(progress, startVal, endVal - startVal, this.duration);
        val = val > endVal ? endVal : val
      }
      let finalVal = this.substrNum(val)
      if (progress < this.duration) {
        requestAnimationFrame(callback)
      }
      return finalVal
    }
  }
};
</script>

<style lang="sass" scoped>
  @import '../sass/setting.sass'

  #BarWithTag
    .score-box
      width: 100%
      &.flex
        flex-wrap: wrap
      > .bar-box
        width: calc(100% / 2 - 2rem)
        padding: 1rem
        .score-title
          color: black

        .bar-content
          &.flex
            align-items: center
          > span
            font-size: 2rem
            margin-left: .7rem
            color: $keyColor_1

        .bar-backing
          width: 100%
          height: 3px
          background-color: rgba(0, 0, 0, 0.2)
          .bar
            position: relative
            width: 40%
            height: 3px
            background-color: $keyColor_1
            transition: width 1s
            .tip
              position: absolute
              top: 8px
              right: 0
              font-size: .5rem
              letter-spacing: 1px
              color: white
              background-color: #282828
              border-radius: 3px
              padding: 5px 15px
              transform: translateX(50%)
              span
                display: inline-block
                transform: scale(0.9)
                white-space: nowrap

</style>
