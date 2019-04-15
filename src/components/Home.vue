<template>
  <div class="home">
    <div class="home__slider slider slider--vertical">
      <span class="slider__line">
        <span class="slider__fill"></span>
        <span class="slider__handle"></span>
      </span>
      <span class="slider__label slider__label--max">Max</span>
      <span class="slider__label slider__label--min">Min</span>
    </div>
    <main class="keyboard__list">
      <button class="keyboard__add-button button button--icon button--primary icon--add"><span>Add layer</span></button>
      <div v-for="ghost in uppers" class="keyboard keyboard--ghost keyboard--ghost-upper">
        <ul class="keyboard__keys">
          <li v-for="(key, i) in 48" class="keyboard__key key" :class="`key--${i}`"></li>
        </ul>
      </div>
      <div class="keyboard">
        <ul class="keyboard__keys">
          <li v-for="(key, i) in keys" class="keyboard__key key" :class="`key--${i}`">
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

export default {
  name: 'home',
  data () {
    return {
      keys: keymap,
      rowAmount: 4,
      uppers: 0,
      lowers: 0,
    }
  },
  computed: {
    rows() {
      return []
    },
  },
}
</script>
