<template>
  <div class="container-fluid center">
    <div class="center__child">
      <!-- <logo /> -->
      <section>
        <canvas id="thumbnail" />
      </section>
      <section>
        <b-form>
          <b-form-group
            label-cols-sm="4"
            label="Font-Family"
            label-align-sm="right"
            label-for="fontFamliy"
          >
            <b-form-select
              id="fontFamliy"
              :value="fontFamily"
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
              :value="fontSize"
              :options="fontSizeList"
            />
          </b-form-group>
          <b-form-group
            label-cols-sm="4"
            label="bgColor"
            label-align-sm="right"
            label-for="Color"
          >
            <chrome-picker v-model="colors" />
          </b-form-group>
        </b-form>
      </section>
    </div>
  </div>
</template>

<script>
import { Chrome } from 'vue-color'

export default {
  components: {
    'chrome-picker': Chrome
  },
  data () {
    return {
      fontFamilyList: {
        'Noto Sans KR': 'Noto Sans KR',
        'Nanum Gothic': 'Nanum Gothic',
        'Nanum Myeongjo': 'Nanum Myeongjo',
        'Helvetica': 'Helvetica',
        'sans-serif': 'sans-serif'
      },
      fontFamily: 'Noto Sans KR',
      fontSizeList: {
        14: '14px',
        18: '18px',
        24: '24px',
        28: '28px',
        32: '32px'
      },
      fontSize: 28,
      colors: ''
    }
  }
}
</script>

<style lang="scss" scoped>
.center {
  display: flex;
  justify-content: center;
  align-items: center;
}

#thumbnail {
  border: 1px solid red;
}
</style>
