<template>
  <div class="p-quiz">
    <div class="c-container">
      <div class="p-quiz__body">
        <h2 class="c-title01">問題を選択</h2>
        <ul class="p-quiz__body__list">
          <li v-for="(page, index) in data" :key="page.key">
            <nuxt-link :to="`/quiz/${page.id}`">{{ page.title }}</nuxt-link>
          </li>
          <!-- /.p-quiz__body__list -->
        </ul>
        <!-- /.p-quiz__body -->
      </div>
      <!-- /.p-quiz -->
    </div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
interface Data {
  data: {}
}
export default Vue.extend({
  async asyncData({ app, error, redirect }) {
    try {
      const response = await app.$axios.$get(`/data.json`)
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
  created() {},
})
</script>
<style lang="scss" scoped>
@use '@/assets/sass/foundation/' as f;
.p-quiz {
  padding-top: f.smooth_size(30px, 40px);
  &__body {
    &__list {
      display: flex;
      align-items: center;
      justify-content: center;
      flex-wrap: wrap;
      li {
        width: 50%;
        text-align: center;
        padding: f.smooth_size(8px, 15px) f.smooth_size(10px, 20px);
        a {
          display: flex;
          justify-content: center;
          align-items: center;
          padding: f.smooth_size(30px, 60px);
          font-weight: bold;
          border: 1px solid #000;
          transition: all 0.3s ease;
          &:hover {
            color: #fff;
            background: #000;
          }
        }
      }
    }
  }
}
</style>
