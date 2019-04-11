<template>
  <div class="home">
    <h1>Configure your keyboard</h1>
    <main class="keyboard">
      <ul class="keyboard__keys">
        <li v-for="key in keys" class="keyboard__key key">
          <span class="key__title">{{ key.name }}</span>
          <span class="key__desc">{{ key.code }}</span>
        </li>
      </ul>
    </main>
  </div>
</template>

<script>
export default {
  name: 'home',
  data () {
    return {
      keys: [],
      rowAmount: 4,
    }
  },
  mounted() {
    for (let i = 0; i < 40; i++) {
      this.keys.push({
        name: 'A',
        code: 'KC_A',
      })
    }
  },
  computed: {
    rows() {
      return []
    },
  },
}
</script>
