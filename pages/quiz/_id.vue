<template>
  <div class="p-quiz">
    <div class="c-container">
      <StringProblem v-if="data.type === 'string'" v-bind:DataObj="data" />
      <ArrayProblem v-else v-bind:DataObj="data" />
    </div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
import axios from 'axios'
import StringProblem from '@/components/StringProblem.vue'
import ArrayProblem from '@/components/ArrayProblem.vue'
interface Data {
  data: {}
}
export default Vue.extend({
  components: {
    StringProblem,
    ArrayProblem,
  },
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
  props: {
    DataObj: {
      type: Object,
      default: () => ({}),
    },
    Type: {
      type: String,
      default: () => '',
    },
  },
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
