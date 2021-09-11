<template>
  <div class="p-index">
    <div class="p-index__body">
      <h1 class="p-index__title">FootBall Quiz</h1>
      <div class="c-button01"><nuxt-link to="quiz">Start</nuxt-link></div>
      <!-- /.p-index__body -->
    </div>
    <!-- /.p-index -->
  </div>
</template>

<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
  data() {
    return {}
  },
})
</script>
<style lang="scss" scoped>
@use '@/assets/sass/foundation/' as f;
.p-index {
  font-size: f.smooth_font(20px, 40px);
  background: url('/bg.png');
  background-size: cover;
  &__body {
    width: 100vw;
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    font-family: f.$en_font;
    color: #fff;
  }
}
</style>
