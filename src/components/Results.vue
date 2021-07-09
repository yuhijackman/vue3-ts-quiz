<template>
  <div class="result">
    <div class="title">{{ result.title }}</div>
    <div class="desc">
        {{ result.desc }}
    </div>
  </div>
</template>


<script lang="ts">
import { defineComponent, computed, PropType } from 'vue'
import { Result } from '../data';

export default defineComponent({
  emits: ['onClickAnswer'],
  props: {
    results: {
      type: Array as PropType<Result[]>,
      required: true,
    },
    correctAnswer: {
      type: Number,
      required: true,
    }
  },
  setup(props) {
    const result = computed(() => {
      return props.results.find((result) => {
        return result.min <= props.correctAnswer && props.correctAnswer <= result.max
      });
    });

    return {
      result
    }
  },
})
</script>
