<template>
  <button class="btn" :style="{ background: color }" @click="onClick()">
    {{ text }}
  </button>
</template>
<script lang="ts">
import { defineComponent } from 'vue'
import type { PropType } from 'vue'
export default defineComponent({
  name: 'ButtonComp',
  props: {
    text: {
      type: String as PropType<string>,
      default: () => '',
    },
    color: {
      type: String as PropType<string>,
      default: () => '',
    },
  },
  emits: ['btn-click'],
  methods: {
    onClick() {
      this.$emit('btn-click')
    },
  },
})
</script>
