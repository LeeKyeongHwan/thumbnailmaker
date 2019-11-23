<template>
  <div class="container-fluid">
    <section class="thumbnail_wrap text-center">
      <thumbnail-canvas
        :text="text"
        :font-family="fontFamily"
        :font-size="fontSize"
        :width="width"
        :height="height"
        :file="file"
        :hex-color="hexColor"
      />
    </section>
    <section class="form_wrap">
      <b-form>
        <b-form-group
          label-cols-sm="4"
          label="Text"
          label-align-sm="right"
          label-for="text"
        >
          <b-form-input id="text" v-model="text" placeholder="text" />
        </b-form-group>
        <b-form-group
          label-cols-sm="4"
          label="Font-Family"
          label-align-sm="right"
          label-for="fontFamliy"
        >
          <b-form-select
            id="fontFamliy"
            v-model.number="fontFamily"
            :options="fontFamilyList"
          />
        </b-form-group>
        <b-form-group
          label-cols-sm="4"
          label="Font-Size"
          label-align-sm="right"
          label-for="fontSize"
        >
          <b-form-select
            id="fontSize"
            v-model.number="fontSize"
            :options="fontSizeList"
          />
        </b-form-group>
        <b-form-group
          label-cols-sm="4"
          label="Width"
          label-align-sm="right"
          label-for="width"
        >
          <b-input-group append="px">
            <b-form-input id="width" v-model.number="width" placeholder="width" />
          </b-input-group>
        </b-form-group>
        <b-form-group
          label-cols-sm="4"
          label="Height"
          label-align-sm="right"
          label-for="height"
        >
          <b-input-group append="px">
            <b-form-input id="height" v-model.number="height" placeholder="height" />
          </b-input-group>
        </b-form-group>
        <b-form-group
          label-cols-sm="4"
          label="bg-image"
          label-align-sm="right"
          label-for="bgImgFile"
        >
          <b-form-file
            id="bgImgFile"
            v-model="file"
            placeholder="Choose a file or drop it here..."
            drop-placeholder="Drop file here..."
          />
        </b-form-group>
        <b-form-group
          label-cols-sm="4"
          label="bg-color"
          label-align-sm="right"
          label-for="Color"
        >
          <chrome-picker :value="colors" @input="updateColors" />
        </b-form-group>

        <div>
          <b-button block variant="primary" @click="downloadImg">
            Download
          </b-button>
        </div>
      </b-form>
    </section>
  </div>
</template>

<script>
import { Chrome } from 'vue-color'
import ThumbnailCanvas from '~/components/ThumbnailCanvas'

export default {
  name: 'Index',
  components: {
    'chrome-picker': Chrome,
    ThumbnailCanvas
  },
  data () {
    return {
      ctx: null,
      text: 'Thumnbnail-maker 👍',
      fontFamilyList: {
        'Roboto': 'Roboto',
        'Noto Sans KR': 'Noto Sans KR',
        'Nanum Gothic': 'Nanum Gothic',
        'Nanum Myeongjo': 'Nanum Myeongjo',
        'Helvetica': 'Helvetica',
        'sans-serif': 'sans-serif'
      },
      fontFamily: 'Noto Sans KR',
      fontSizeList: {
        28: '28px',
        36: '36px',
        42: '42px',
        50: '50px',
        60: '60px'
      },
      fontSize: 42,
      width: 600,
      height: 300,
      file: null,
      colors: '',
      hexColor: ''
    }
  },
  mounted () {
    this.getRandomColor()
  },
  methods: {
    downloadImg () {
      const canvas = document.getElementById('thumbnail')
      const url = canvas.toDataURL('image/png')
      const a = document.createElement('a')
      a.href = url
      a.download = 'download.png'
      a.click()
    },
    updateColors (colors) {
      this.hexColor = colors.hex
    },
    getRandomColor () {
      this.$nextTick(() => {
        const color = '#' + Math.floor(Math.random() * 16777215).toString(16)
        this.colors = color
        this.hexColor = color
      })
    }
  }

}
</script>

<style lang="scss" scoped>
.container-fluid { padding: 1rem; }
.thumbnail_wrap { margin-bottom: 1rem; }
#thumbnail { margin: 0 auto; }
.form_wrap {
  margin: 0 auto;
  min-width: 344px;
  max-width: 600px;
}
</style>
