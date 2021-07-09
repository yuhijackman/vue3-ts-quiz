<template>
  <div class="progress">
      <div
        class="bar"
        :style="{width: barWidth}"
      ></div>
      <div class="status">{{ answeredQuestion }} out of {{ questionLength }} questions answered</div>
  </div>
</template>

<script lang="ts">
import { defineComponent, computed } from 'vue'

export default defineComponent({
  emits: ['onClickAnswer'],
  props: {
    answeredQuestion: {
      type: Number,
      required: true,
    },
    questionLength: {
      type: Number,
      required: true,
    }
  },
  setup(props) {
    const barWidth = computed(() => {
      return `${(props.answeredQuestion / props.questionLength) * 100}%`
    })
    return {
      barWidth,
    }
  },
})
</script>
