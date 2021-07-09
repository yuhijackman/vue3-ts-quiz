<template>
  <section>
    <div class="single-question">
      <div class="question">{{ visibleQuestion.q }}</div>
      <div class="answers">
          <div
            class="answer"
            v-for="answer in visibleQuestion.answers"
            :key="answer.text"
            @click="$emit('onClickAnswer', answer)"
          >
            {{ answer.text }}
          </div>
      </div>
    </div>
  </section>
</template>

<script lang="ts">
import { defineComponent, PropType, computed } from 'vue'
import { Question } from '../data';

export default defineComponent({
  emits: ['onClickAnswer'],
  props: {
    questions: {
      type: Object as PropType<Question[]>,
      required: true
    },
    answeredQuestion: {
      type: Number,
      default: 0,
    }
  },
  setup(props) {
    const visibleQuestion = computed(() => {
      return props.questions[props.answeredQuestion];
    })
    
    return {
      visibleQuestion
    }
  },
})
</script>
