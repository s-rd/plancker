<template>
  <div
    class="key"
    :class="keyStyle"
    :ref="`key--${index}`"
    @click="dragging = true"
  >
    <span class="key__name">{{ name }}</span>
    <span class="key__code">{{ code }}</span>
  </div>
</template>

<script>
export default {
  name: 'key',
  props: {
    keyData: {
      type: Object,
      required: true,
    },
    dragging: {
      type: Boolean,
      required: false,
      default: false,
    },
  },
  data() {
    return this.keyData
  },
  computed: {
    keyStyle() {
      const dragging = this.dragging && 'key--placeholder'
      const empty = !this.keyData && 'key--empty'
      const index = `key--${this.index}`
      return [ dragging, empty, index ]
    },
  },
}
</script>
