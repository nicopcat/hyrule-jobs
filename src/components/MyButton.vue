<template>
  <div>
    <button :style="{ fontSize: `${size}px`, backgroundColor: bgcolor, color:color , padding: myPadding}">{{ text }}</button>
  </div>
</template>

<script lang="ts">
import { defineComponent, PropType } from 'vue'

export default defineComponent({
  props: {
    text: {
      required: true,
      type: String,
      default: 'Button'
    },
    size: {
      required: false,
      type: Number,
      default: 12
    },
    bgcolor: {
      required: false,
      type: String,
      default: '#fff'
    },
    color: {
      required: false,
      type: String,
      default: '#1195c9'
    },
    myPadding:{
      required: false,
      type: [Number, String] as PropType<number | string>,
      default: '8px 10px'
    },
  },
  setup (props) {

    return {}
  }
})
</script>

<style scoped>
  button {
    margin: 0 10px;
    color: #1195c9;
    border: 3px solid #1195c9;
    background: #d5f0ff;
    /* padding: 8px 16px; */
    border-radius: 4px;
    cursor: pointer;
    font-weight: bold;
  }
</style>