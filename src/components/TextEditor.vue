<template>
  <div ref="text-editor" class="text-editor">Hey</div>
</template>

<script>
export default {
  mounted() {
    this.$refs['text-editor'].contentEditable = true
  }
}
</script>

<style lang="scss">
.text-editor {
  margin: 1.5rem;
  padding: 0.5rem;
  border: 5px solid black;
  border-radius: 10px;
  font-size: 1.5rem;
  overflow-y: auto;
  &:focus {
    outline: none;
  }
}
</style>
