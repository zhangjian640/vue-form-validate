<template>
  <div class="c-form">
    <slot></slot>
  </div>
</template>

<script>
  export default {
    name: 'CForm',
    provide() {
      return {
        form: this // 将this传递给子组件，命名为form
      }
    },
    props: {
      model: { type: Object, required: true },
      rules: { type: Object }
    },
    methods: {
      async validate(callback) {
        const tasks = this.$children
          .filter(item => item.prop) // 过滤有prop的子组件
          .map(item => item.validate()) // 执行校验，返回Promise
        const result = await Promise.all(tasks) // 执行异步
        if (result.some(validate => !validate)) { // 检验是否包含false的验证
          callback(false)
        } else {
          callback(true)
        }
      }
    }
  }
</script>

<style scoped>
</style>
