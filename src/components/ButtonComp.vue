<template>
  <button class="btn" :style="{ background: color }" @click="onClick()">
    {{ text }}
  </button>
</template>
<script>
export default {
  name: 'ButtonComp',
  props: {
    text: {
      type: String,
      default: () => '',
    },
    color: {
      type: String,
      default: () => '',
    },
  },
  emits: ['btn-click'],
  methods: {
    onClick() {
      this.$emit('btn-click');
    },
  },
};
</script>
