<template>
  <nav class="nav">
    <router-link :to="{ name: 'home' }" class="nav__logo">Plancker</router-link>
  </nav>
</template>

<script>
export default {
  name: 'menu-bar',
}
</script>
