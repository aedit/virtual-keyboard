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
      text: '',
      startText:
        'Hi, I am Udit Sen. I am a Frontend Developer.\nYou can check out my portfolio at https://aedit.me\nThis is a fun keyboard I have developed using Vue.js.\nMy github: https://github.com/aedit --- My Linkedin: https://linkedin.com/in/aedit\nFor useful shortcuts hit CTRL + T\nHit any key to get started',
      allowTyping: false,
      firstStroke: true
    }
  },
  components: { KeyBoard },
  mounted() {
    this.initalizeStartText()
  },
  methods: {
    checkFirstStroke() {
      if (this.firstStroke) {
        this.text = ''
        this.firstStroke = false
      }
    },
    handleKeyStroke(evt) {
      if (this.allowTyping) {
        this.checkFirstStroke()
        this.text += evt
      }
    },
    handleBackspace() {
      if (this.allowTyping) {
        this.checkFirstStroke()
        this.text = this.text.slice(0, -1)
      }
    },
    initalizeStartText() {
      let index = 0
      let interval = setInterval(() => {
        this.text += this.startText[index++]
        if (index === this.startText.length) {
          clearInterval(interval)
          this.allowTyping = true
        }
      }, 50)
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
