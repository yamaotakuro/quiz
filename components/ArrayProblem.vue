<template>
  <div class="p-quiz__body">
    <h2 class="c-title01">{{ DataObj.title }}</h2>
    <div class="p-quiz__body__problrem">
      {{ DataObj.problem }}
    </div>
    <draggable
      tag="ul"
      class="p-quiz__body__list"
      v-model="list"
      @start="drag = true"
      @end="onEnd"
    >
      <li v-for="(data, index) in list" :key="data.index">
        <img :src="`${data.url}`" alt="" />
        <span>{{ data.name }}</span>
      </li>
    </draggable>
    <div class="c-button01 -black">
      <nuxt-link
        :to="`/quiz/answer/${this.$route.params.id}?answer_array=${this.answerArray}`"
        >回答する</nuxt-link
      >
    </div>
    <!-- /.p-quiz__body -->
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
import axios from 'axios'
import draggable from 'vuedraggable'

export default Vue.extend({
  components: {
    draggable,
  },
  props: ['DataObj'],
  data() {
    return {
      answer: '' as string,
      list: this.DataObj.body as [],
      answerArray: this.DataObj.body as [],
    }
  },
  methods: {
    onEnd() {
      const array: [] = []
      this.list.forEach((element: string) => {
        array.push(element.name)
      })
      array.join(',')
      this.answerArray = array
    },
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
    &__list {
      margin: f.smooth_size(20px, 40px) auto;
      display: flex;
      justify-content: space-between;
      li {
        text-align: center;
        cursor: grab;
        padding: f.smooth_size(20px, 30px);
        span {
          display: block;
        }
      }
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
