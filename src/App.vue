<template>
  <div id="app">
    <Player/>
  </div>
</template>

<script>
import Player from './components/Player.vue'

export default {
  name: 'App',
  components: {
    Player
  }
}
</script>

<style lang="scss">
@import "~@/assets/scss/vendors/bootstrap-vue/index";

</style>
