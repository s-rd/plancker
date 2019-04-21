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
      <div v-for="ghost in uppers" class="keyboard keyboard--ghost keyboard--ghost-upper">
        <ul class="keyboard__keys">
          <li v-for="(key, i) in 48" class="keyboard__key key" :class="`key--${i}`"></li>
        </ul>
      </div>
      <div class="keyboard">
        <ul class="keyboard__keys" :style="keyboardTiltStyle">
          <li v-for="(key, i) in keys" class="keyboard__key key" :class="`key--${i}`" :ref="`key--${i}`">
            <span class="key__name">{{ key.name }}</span>
            <span class="key__code">{{ key.code }}</span>
          </li>
        </ul>
      </div>
      <div v-for="ghost in lowers" class="keyboard keyboard--ghost keyboard--ghost-lower">
        <ul class="keyboard__keys">
          <li v-for="(key, i) in 48" class="keyboard__key key" :class="`key--${i}`"></li>
        </ul>
      </div>
      <button class="keyboard__add-button button button--icon icon--add"><span>Add layer</span></button>
    </main>

  </div>
</template>

<script>
import keymap from '@/assets/keymaps/semonje'
import VerticalSlider from '@/components/VerticalSlider'

export default {
  name: 'home',
  components: {
    VerticalSlider,
  },
  data () {
    return {
      keys: keymap,
      rowAmount: 4,
      uppers: 0,
      lowers: 0,
      slider: {
        value: 50,
        min: 0,
        max: 100,
      },
    }
  },
  mounted() {
    this.addEventListeners()
  },
  destroyed() {
    this.removeEventListeners()
  },
  methods: {
    handleDrag(e) {
      if (!e.target && !e.target.classList.contains('key')) return
      e.preventDefault()
      console.log('heisann', e)
      e.target.classList.add('key--drag')
    },
    addEventListeners() {
      document.addEventListener('mousedown', this.handleDrag)
      document.addEventListener('mouseup', this.stopDrag)
      document.addEventListener('mousemove', this.drag)
    },
    removeEventListeners() {
      document.removeEventListener('mousedown', this.handleDrag)
      document.removeEventListener('mouseup', this.stopDrag)
      document.removeEventListener('mousemove', this.drag)
    },
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
    keyboardTiltStyle() {
      return { transform: `rotateX(${this.keyboardTilt}deg)`}
    },
    sliderLabel() {
      const deg = Math.floor(this.keyboardTilt)
      return `${deg}° degrees`
    },
  },
}
</script>
