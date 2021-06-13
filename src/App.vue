<template>
  <div :key="reloadKey" id="app">
    <div class="text-editor">
      <textarea ref="text-area" readonly :value="text" />
    </div>
    <KeyBoard
      @keyStroke="handleKeyStroke"
      @backspace="handleBackspace"
      @ctrlClicked="handleCtrlClick"
      :randomizeKeys="randomizeKeys"
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
        'Hi, I am Udit Sen. I am a Frontend Developer.\nYou can check out my portfolio at https://aedit.me\nThis is a fun keyboard I have developed using Vue.js.\nMy github: https://github.com/aedit --- My Linkedin: https://linkedin.com/in/aedit\nFor useful shortcuts hit CTRL + I\nHit any key to get started',
      infoText:
        'CTRL + S -> Save\t\tCTRL + A -> Select All\nCTRL + C -> Copy\t\tCTRL + X -> Cut\nCTRL + V -> Paste\t\tCTRL + Q -> Clear All\nCTRL + I -> Info\t\tCTRL + D -> Delete Save\nCTRL + R -> Toggle Randomization\n\t\tCTRL + U -> Udit Sen',
      allowTyping: false,
      firstStroke: true,
      randomizeKeys: true,
      reloadKey: 0
    }
  },
  components: { KeyBoard },
  mounted() {
    if (window.localStorage.getItem('virtual-keyboard-data')) {
      this.text = window.localStorage.getItem('virtual-keyboard-data')
      this.allowTyping = true
      this.firstStroke = true
    } else this.initalizeStartText()
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
      this.updateScroll()
    },
    handleBackspace() {
      if (this.allowTyping) {
        this.checkFirstStroke()
        this.text = this.text.slice(0, -1)
      }
      this.updateScroll()
    },
    handleCtrlClick(evt) {
      if (!this.allowTyping) return
      switch (evt.upper) {
        case 'A':
          this.$refs['text-area'].select()
          return
        case 'S':
          this.saveText()
          return
        case 'D':
          this.deleteText()
          return
        case 'Q':
          this.text = ''
          return
        case 'U':
          this.text = this.startText
          return
        case 'I':
          this.text = this.infoText
          return
        case 'C':
          document.execCommand('copy')
          return
        case 'X':
          document.execCommand('copy')
          this.text = ''
          return
        case 'V':
          navigator.clipboard.readText().then((el) => (this.text += el))
          return
        case 'R':
          this.randomizeKeys = !this.randomizeKeys
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
    },
    updateScroll() {
      this.$refs['text-area'].scrollTop = this.$refs['text-area'].scrollHeight
    },
    saveText() {
      window.localStorage.setItem('virtual-keyboard-data', this.text)
    },
    deleteText() {
      window.localStorage.removeItem('virtual-keyboard-data')
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
