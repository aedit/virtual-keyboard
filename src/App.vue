<template>
  <div id="app">
    <div class="text-editor">
      <textarea ref="text-area" readonly :value="text" />
    </div>
    <KeyBoard
      @keyStroke="handleKeyStroke"
      @backspace="handleBackspace"
    ></KeyBoard>
  </div>
</template>

<script>
import KeyBoard from '@/components/KeyBoard'

export default {
  name: 'App',
  data() {
    return {
      text: ''
    }
  },
  components: { KeyBoard },
  methods: {
    handleKeyStroke(evt) {
      this.text += evt
    },
    handleBackspace() {
      this.text = this.text.slice(0, -1)
    }
  }
}
</script>

<style lang="scss">
#app {
  display: grid;
  grid-template-rows: 1fr 1fr;
}
</style>
