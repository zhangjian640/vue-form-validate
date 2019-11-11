<template>
  <div class="c-input">
    <input :value="value" :type="type" @input="inputHandle">
  </div>
</template>

<script>
  export default {
    name: 'CInput',
    props: {
      type: {
        type: String,
        default: 'text'
      },
      value: {
        type: String
      }
    },
    methods: {
      inputHandle(e) {
        this.$emit('input', e.target.value)
        this.$parent.$emit('validate')
      }
    }
  }
</script>

<style scoped>
</style>
