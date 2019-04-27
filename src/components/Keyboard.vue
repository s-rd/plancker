<template>
  <div class="keyboard">

    <ul class="keyboard__keys" :style="keyboardTiltStyle" ref="key-wrapper">
      <key
        v-for="(key, index) in keys"
        :key="index"
        :key-data="{ ...key, index }"
        class="keyboard__key"
      />
    </ul>

  </div>
</template>

<script>
import Key from '@/components/Key'

export default {
  name: 'keyboard',
  components: {
    Key,
  },
  props: {
    keys: {
      type: Array,
      required: true,
    },
    tilt: {
      type: Number,
      required: false,
      default: 25,
    },
  },
  data() {
    return {
      dragging: false,
      draggingEl: null,
      draggingOffsetTop: 0,
      draggingOffsetLeft: 0,
    }
  },
  mounted() {
    this.addEventListeners()
    this.draggingOffsetTop = this.$refs['key-wrapper'].offsetTop
    this.draggingOffsetLeft = this.$refs['key-wrapper'].offsetLeft
  },
  destroyed() {
    this.removeEventListeners()
  },
  methods: {
    handleDrag(e) {
      if (!e.target || !e.target.classList.contains('key')) return
      e.preventDefault()
      this.draggingEl = e.target
      this.dragging = true
    },
    drag(e) {
      if (!this.dragging) return
      this.draggingEl.classList.add('key--drag')
      const top = `${e.clientY - 500}px`
      const left = `${e.clientX - 450}px`
      this.draggingEl.style.top = top
      this.draggingEl.style.left = left
    },
    stopDrag(e) {
      if (!this.dragging) return
      e.preventDefault()
      this.draggingEl.classList.remove('key--drag')
      this.draggingEl = null
      this.dragging = false
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
    keyboardTiltStyle() {
      return { transform: `rotateX(${this.tilt}deg)`}
    },
  },
}
</script>
