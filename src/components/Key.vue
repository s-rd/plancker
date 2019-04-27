<template>
  <li class="key" :class="`key--${index}`" :ref="`key--${index}`">
    <span class="key__name">{{ name }}</span>
    <span class="key__code">{{ code }}</span>
  </li>
</template>

<script>
export default {
  name: 'key',
  props: {
    keyData: {
      type: Object,
      required: true,
    },
  },
  data() {
    return this.keyData
  },
}
</script>
