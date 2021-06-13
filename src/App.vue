<template>
  <div id="app">
    <TextEditor :text="text"></TextEditor>
    <KeyBoard
      @keyStroke="handleKeyStroke"
      @backspace="handleBackspace"
    ></KeyBoard>
  </div>
</template>

<script>
import TextEditor from '@/components/TextEditor'
import KeyBoard from '@/components/KeyBoard'

export default {
  name: 'App',
  data() {
    return {
      text: ''
    }
  },
  components: { TextEditor, KeyBoard },
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
