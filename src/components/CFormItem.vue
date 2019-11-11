<template>
  <div class="c-form-item">
    <span>{{label}}</span>
    <slot></slot>
    <p :class="{'error' : errorMessage}">{{errorMessage}}</p>
  </div>
</template>

<script>
  import Validator from 'async-validator'

  export default {
    name: 'CFormItem',
    inject: ['form'],
    props: ['label', 'prop'],
    created() {
      this.$on('validate', this.validate)
    },
    data() {
      return { errorMessage: '' }
    },
    methods: {
      validate() {
        return new Promise(resolve => {
          const descriptor = { [this.prop]: this.form.rules[this.prop] }
          const validator = new Validator(descriptor)
          validator.validate({ [this.prop]: this.form.model[this.prop] }, (errors) => {
            if (errors) {
              this.errorMessage = errors[0].message
              resolve(false)
            } else {
              this.errorMessage = ''
              resolve(true)
            }
          })
        })
      }
    }
  }
</script>

<style scoped>
  .error {
    color: red;
    font-size: 12px;
  }
</style>
