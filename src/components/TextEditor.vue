<template>
  <div ref="text-editor" class="text-editor">
    <textarea readonly :value="text" />
  </div>
</template>

<script>
export default {
  props: {
    text: {
      required: true,
      type: String
    }
  }
}
</script>

<style lang="scss">
.text-editor {
  margin: 1.5rem;

  textarea {
    resize: none;
    width: 100%;
    height: 90%;
    padding: 0.5rem;
    border: 5px solid black;
    border-radius: 10px;
    font-size: 1.5rem;

    &:focus {
      outline: none;
    }
  }
}
</style>
