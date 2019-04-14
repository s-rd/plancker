<template>
  <div class="home">
    <main class="keyboard__list">
      <div class="keyboard keyboard--ghost keyboard--ghost-upper">
        <ul class="keyboard__keys">
          <li v-for="key in 48" class="keyboard__key key"></li>
        </ul>
      </div>
      <div class="keyboard">
        <ul class="keyboard__keys">
          <li v-for="key in keys" class="keyboard__key key">
            <span class="key__name">{{ key.name }}</span>
            <span class="key__code">{{ key.code }}</span>
          </li>
        </ul>
      </div>
      <div class="keyboard keyboard--ghost keyboard--ghost-lower">
        <ul class="keyboard__keys">
          <li v-for="key in 48" class="keyboard__key key"></li>
        </ul>
      </div>
    </main>
  </div>
</template>

<script>
import keymap from '@/assets/keymaps/semonje'

export default {
  name: 'home',
  data () {
    return {
      keys: keymap,
      rowAmount: 4,
    }
  },
  computed: {
    rows() {
      return []
    },
  },
}
</script>
