<template>
  <canvas
    id="thumbnail"
    ref="canvas"
    :width="width"
    :height="height"
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
      type: File,
      default: null
    },
    hexColor: {
      type: String,
      default: ''
    }
  },
  data () {
    return {
      canvas: null,
      bgFile: null
    }
  },
  watch: {
    width () {
      this.paint()
    },
    height () {
      this.paint()
    },
    text () {
      this.paint()
    },
    fontFamily () {
      this.paint()
    },
    fontSize () {
      this.paint()
    },
    hexColor () {
      this.paint()
    },
    file (file) {
      this.bgFile = file
      this.paint()
    }
  },
  mounted () {
    this.init()
    this.paint()
  },
  methods: {
    init () {
      this.canvas = this.$refs.canvas
    },
    paint () {
      this.$nextTick(() => {
        // FIXME: 이미지 로드되는 순서 동기화 시켜야 함
        this.setBgColor()
        this.setImage()
        this.setText()
      })
    },
    setText () {
      const ctx = this.canvas.getContext('2d')
      ctx.textAlign = 'center'
      ctx.textBaseline = 'middle'
      ctx.font = `${this.fontSize}px ${this.fontFamily}`
      ctx.fillStyle = 'white'
      ctx.fillText(this.text, this.canvas.width / 2, this.canvas.height / 2)
    },
    setBgColor () {
      const ctx = this.canvas.getContext('2d')
      ctx.fillStyle = this.hexColor
      ctx.fillRect(0, 0, this.width, this.height)
    },
    setImage () {
      const file = this.bgFile

      if (!file) {
        return
      }

      const reader = new FileReader()
      reader.readAsDataURL(file)
      reader.onload = () => {
        const ctx = this.canvas.getContext('2d')

        const img = new Image()
        img.src = reader.result
        img.onload = () => {
          // 가운데 정렬
          const x = this.canvas.width / 2 - img.width / 2
          const y = this.canvas.height / 2 - img.height / 2
          ctx.drawImage(img, x, y)
        }

        // FIXME: object-fit: cover
        /* const ratio = img.width / img.height
        let newWidth = this.canvas.width
        let newHeight = newWidth / ratio
        if (newHeight < this.canvas.height) {
          newHeight = this.canvas.height
          newWidth = newHeight * ratio
        }
        const xOffset = newWidth > this.canvas.width ? (this.canvas.width - newWidth) / 2 : 0
        const yOffset = newHeight > this.canvas.height ? (this.canvas.height - newHeight) / 2 : 0
        ctx.drawImage(img, xOffset, yOffset, newWidth, newHeight) */
      }
    }
  }
}
</script>

<style>
</style>
