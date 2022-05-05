<template>
  <terminalBg />
  <div id="main">
    <HomeView />
  </div>
</template>

<script>
import terminalBg from '@/components/terminalBg.vue'
import HomeView from '@/components/HomeView.vue'
export default {
  components: {
    terminalBg,
    HomeView
  }
}
</script>

<style lang="scss">
body {
  background: $dark_blue;
  overflow: hidden;
}
#main {
  width: 100vw;
  height: 100vh;
  z-index: 10;
}

* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}
</style>
