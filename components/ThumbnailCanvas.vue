<template>
  <canvas
    id="thumbnail"
    ref="canvas"
    :style="{
      width: `${width}px`,
      height: `${height}px`
    }"
  />
</template>

<script>
export default {
  name: 'ThumbnailCanvas',
  props: {
    width: {
      type: Number,
      default: 600
    },
    height: {
      type: Number,
      default: 400
    },
    text: {
      type: String,
      default: ''
    },
    fontFamily: {
      type: String,
      required: true,
      default: ''
    },
    fontSize: {
      type: Number,
      required: true,
      default: 28
    },
    file: {
      type: Object,
      default: null
    },
    colors: {
      type: Object,
      default: null
    }
  },
  watch: {
    text () {
      this.setText()
    },
    fontFamily () {
      this.setText()
    },
    fontSize () {
      this.setText()
    },
    file () {},
    colors: {
      deep: true,
      handler (newValue, oldValue) {
        this.setBgColor()
      }
    }
  },
  mounted () {
    this.ctx = this.$refs.canvas.getContext('2d')
    this.init()
  },
  methods: {
    init () {},
    setText () {
      this.ctx.font = `${this.fontSize}px ${this.fontFamily}`
      this.ctx.fillText(this.text, 10, 50)
    },
    setBgColor () {
      this.ctx.fillStyle = this.colors.hex || '#54ABCA'
      this.ctx.fillRect(0, 0, this.width, this.height)
    }
  }
}
</script>

<style>
</style>
