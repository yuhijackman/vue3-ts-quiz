<template>
  <div class="ctr">
    <div class="questions-ctr">
      <app-progress
        :answeredQuestion="answeredQuestion"
        :questionLength="questionLength"
      />
      <questions
        v-if="answeredQuestion < questionLength"
        :questions="questions"
        :answeredQuestion="answeredQuestion"
        v-on:onClickAnswer="onClickAnswer"
      />
    </div>
    <app-results
      v-if="answeredQuestion === questionLength"
      :results="results"
      :correctAnswer="correctAnswer"

    />
    <button type="button" class="reset-btn" @click="onReset">Reset</button>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref, watchEffect } from 'vue';
import AppProgress from '@/components/Progress.vue';
import Questions from '@/components/Questions.vue';
import AppResults from '@/components/Results.vue';
import { qData, Data, Question, Answer, Result } from './data';

export default defineComponent({
  name: 'App',
  components: {
    AppProgress,
    Questions,
    AppResults,
  },
  setup() {
    const data: Data = qData;
    const questions: Question[] = data.questions;
    const results: Result[] = data.results;
    const answeredQuestion = ref(0);
    const correctAnswer = ref(0);
    const questionLength = questions.length;

    const onClickAnswer = (answer: Answer) => {
      correctAnswer.value = answer.is_correct ? correctAnswer.value + 1 : correctAnswer.value;
      answeredQuestion.value++;
    }
    const onReset = () => {
      correctAnswer.value = 0;
      answeredQuestion.value = 0;
    }
    return {
      data,
      answeredQuestion,
      questions,
      onClickAnswer,
      correctAnswer,
      questionLength,
      onReset,
      results
    }
  },
});
</script>