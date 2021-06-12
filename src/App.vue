<template>
  <div id="app">
    <TextEditor></TextEditor>
    <KeyBoard></KeyBoard>
  </div>
</template>

<script>
import TextEditor from '@/components/TextEditor'
import KeyBoard from '@/components/KeyBoard'

export default {
  name: 'App',
  components: { TextEditor, KeyBoard }
}
</script>

<style lang="scss">
#app {
  display: grid;
  grid-template-rows: 1fr 1fr;
}
</style>
