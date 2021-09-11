<template>
  <div class="p-quiz__body">
    <h2 class="c-title01">{{ DataObj.title }}</h2>
    <div class="p-quiz__body__problrem">
      {{ DataObj.problem }}
    </div>
    <div class="p-quiz__body__submit">
      <input
        v-model="answer"
        type="text"
        value=""
        placeholder="回答を入力してください"
      />
    </div>
    <div class="c-button01 -black">
      <nuxt-link
        :to="`/quiz/answer/${this.$route.params.id}?answer=${this.answer}`"
        >回答する</nuxt-link
      >
    </div>
    <!-- /.p-quiz__body -->
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
import axios from 'axios'
interface Data {
  data: {}
}
export default Vue.extend({
  props: ['DataObj'],
  data() {
    return {
      data: {} as Data,
      answer: '' as string,
    }
  },
})
</script>
<style lang="scss" scoped>
@use '@/assets/sass/foundation/' as f;
.p-quiz {
  padding-top: f.smooth_size(30px, 40px);
  &__body {
    &__problrem {
      font-size: f.smooth_font(20px, 24px);
    }
    &__submit {
      margin: 30px 0;
      input {
        width: 100%;
        border: 1px solid #ddd;
        padding: f.smooth_size(10px, 20px);
        font-size: f.smooth_font(20px, 24px);
      }
    }
  }
}
</style>
