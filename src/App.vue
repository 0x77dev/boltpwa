<template>
  <div id="app">
      <Bolt />
  </div>
</template>

<script>
import Bolt from './components/Bolt.vue'

export default {
  name: 'app',
  components: {
    Bolt
  }
}
</script>

<style>
#app {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}
</style>
