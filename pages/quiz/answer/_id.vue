<template>
  <div class="p-answer">
    <div class="c-container">
      <div v-if="flg" class="p-answer__body">
        <div class="p-answer__body__text">
          正解！！<br />
          おめでとうございます！
        </div>
        <div class="p-answer__body__img"><img src="/kazu.jpg" alt="" /></div>
        <!-- /.p-answer__body -->
      </div>
      <div v-else class="p-answer__body">
        <div class="p-answer__body__text">
          不正解です・・<br />
          クイズを外すことができるのは、クイズに答える勇気を持つ者だけだ
        </div>
        <div class="p-answer__body__img"><img src="/baggio.jpg" alt="" /></div>
        <!-- /.p-answer__body -->
      </div>
      <!-- /.p-answer -->
      <div class="c-button01 u-center -black">
        <nuxt-link :to="`/quiz`">クイズトップへ</nuxt-link>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import Vue, { PropOptions } from 'vue'
interface Data {
  answer: string
  answer_array: []
}

export default Vue.extend({
  async asyncData({ app, error, route }) {
    try {
      const response = await app.$axios.$get(`/${route.params.id}.json`)

      return { data: response }
    } catch (err) {
      error({
        statusCode: err.response.status,
        message: err.response.data.message,
      })
    }
  },
  data() {
    return {
      data: {} as Data,
    }
  },
  computed: {
    flg(): Boolean {
      if (this.$route.query.answer) {
        const answer: string = this.$route.query.answer
        if (this.data.answer === answer) {
          return true
        } else {
          return false
        }
      } else {
        const str: string = this.$route.query.answer_array

        const answerArray: [] = str.split(',')
        if (JSON.stringify(answerArray) === JSON.stringify(this.data.answer)) {
          return true
        } else {
          return false
        }
      }
    },
  },
})
</script>
<style lang="scss" scoped>
@use '@/assets/sass/foundation/' as f;
.p-answer {
  padding-top: f.smooth_size(30px, 40px);
  &__body {
    display: flex;
    align-items: flex-start;
    justify-content: center;
    &__text {
      font-size: f.smooth_font(16px, 18px);
      border: 1px solid #000;
      background: #fff;
      padding: f.smooth_size(20px, 30px);
      margin-right: f.smooth_size(20px, 40px);
      position: relative;
      &::before,
      &::after {
        content: '';
        position: absolute;
        top: 50%;
        right: 0;
        width: 0;
        height: 0;
        border-style: solid;
        border-width: 10px 0 10px 20px;
        border-color: transparent transparent transparent #fff;
      }
      &::before {
        right: -20px;
        z-index: 10;
      }
      &::after {
        right: -21px;
        z-index: 1;
        border-color: transparent transparent transparent #000;
      }
    }
    &__img {
      width: 30%;
    }
  }
  .c-button01 {
    text-align: center;
    margin-top: 40px;
  }
}
</style>
