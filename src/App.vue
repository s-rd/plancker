<template>
  <div id="app">
    <menu-bar/>
    <router-view/>
  </div>
</template>

<script>
import MenuBar from '@/components/MenuBar'

export default {
  name: 'App',
  components: {
    MenuBar,
  },
}
</script>
