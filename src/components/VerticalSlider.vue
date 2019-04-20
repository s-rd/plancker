<template>
  <div class="slider slider--vertical" :class="sliderClass">
    <span class="slider__line" @click="selectValue" :ref="ref">
      <span class="slider__fill" :style="{ top: topOffset }"/>
      <span class="slider__handle" :style="{ top: topOffset }">
        <span class="slider__handle-label" v-if="customLabel">
          {{ customLabel }}
        </span>
      </span>
    </span>
    <span class="slider__label slider__label--max">Max</span>
    <span class="slider__label slider__label--min">Min</span>
  </div>
</template>

<script>
export default {
  name: 'vertical-slider',
  props: {
    value: {
      type: Number,
      default: 50,
    },
    minValue: {
      type: Number,
      required: false,
      default: 0,
    },
    maxValue: {
      type: Number,
      required: false,
      default: 100,
    },
    customLabel: {
      type: String,
      required: false,
    },
  },
  data() {
    return {
      dragging: false,
      decimal: 0,
      name: 'slider',
    }
  },
  mounted() {
    this.setOffset(this.value)
    this.addEventListeners()
  },
  destroyed() {
    this.removeEventListeners()
  },
  methods: {
    update(value) {
      let newVal = value;

      // Min and max values
      if (newVal < this.minValue && newVal !== '') newVal = this.minValue;
      else if (newVal > this.maxValue) newVal = this.maxValue;

      // Don't set empties
      if (newVal !== '') this.$emit('update:value', newVal)
    },
    startDrag(e) {
      const isRootEl = e.target === this.$el
      const isChild = this.$el.contains(e.target)
      const isOutside = !isRootEl && !isChild

      // Don't start dragging if click is outside
      if (isOutside) return

      this.dragging = true
    },
    stopDrag() {
      if (this.dragging) {
        this.dragging = false
        this.$emit('stopDrag')
      }
    },
    drag(e) {
      if (this.dragging) this.selectValue(e)
    },
    selectValue(e) {
      let pos = e.touches ? e.touches[0].pageY : e.pageY
      let src = this.$refs[this.ref]
      const size = src && src.offsetHeight

      // eslint-disable-next-line
      do {
        pos -= src.offsetTop
      } while ((src = src.offsetParent))

      this.decimal = pos / size
      this.update(this.minValue + Math.round(this.decimal * this.maxValue))
    },
    setOffset(newVal) {
      if (newVal === '') return
      const val = newVal - this.minValue
      const max = this.maxValue - this.minValue
      this.decimal = val / max
    },
    addEventListeners() {
      document.addEventListener('mousedown', this.startDrag)
      document.addEventListener('mouseup', this.stopDrag)
      document.addEventListener('mousemove', this.drag)
    },
    removeEventListeners() {
      document.removeEventListener('mousedown', this.startDrag)
      document.removeEventListener('mouseup', this.stopDrag)
      document.removeEventListener('mousemove', this.drag)
    },
  },
  computed: {
    ref() {
      return `slider-${this.name}`
    },
    topOffset() {
      let dec = this.decimal

      // Min and max values
      if (dec < 0) dec = 0
      else if (dec > 1) dec = 1

      return `${dec * 100}%`
    },
    sliderClass() {
      const dragClass = this.dragging ? ' slider--dragging' : ''
      return dragClass
    },
  },
}
</script>
