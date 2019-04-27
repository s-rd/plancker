<template>
  <div class="home">

    <vertical-slider
      class="home__slider"
      :value.sync="slider.value"
      :min-value="slider.min"
      :max-value="slider.max"
      :custom-label="sliderLabel"
    />

    <main class="keyboard__list">
      <button class="keyboard__add-button button button--icon button--primary icon--add"><span>Add layer</span></button>
      <keyboard :keys="keys" :tilt="keyboardTilt"/>
      <button class="keyboard__add-button button button--icon icon--add"><span>Add layer</span></button>
    </main>

  </div>
</template>

<script>
import keymap from '@/assets/keymaps/semonje'
import VerticalSlider from '@/components/VerticalSlider'
import Keyboard from '@/components/Keyboard'

export default {
  name: 'home',
  components: {
    VerticalSlider,
    Keyboard,
  },
  data () {
    return {
      keys: keymap,
      slider: {
        value: 50,
        min: 0,
        max: 100,
      },
    }
  },
  computed: {
    rows() {
      return []
    },
    keyboardTilt() {
      const val = this.slider.value
      const minTilt = 0
      const maxTilt = 50

      const tilt = val * (maxTilt / this.slider.max)

      return tilt;
    },

    sliderLabel() {
      const deg = Math.floor(this.keyboardTilt)
      return `${deg}° degrees`
    },
  },
}
</script>
