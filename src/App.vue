<template>
  <div id="app">
    <c-form :model="ruleForm" :rules="rules" ref="CForm">
      <c-form-item label="用户名" prop="name">
        <c-input v-model="ruleForm.name"></c-input>
      </c-form-item>
      <c-form-item label="密码" prop="password">
        <c-input type="password" v-model="ruleForm.password"></c-input>
      </c-form-item>
      <button @click="submit('CForm')">新建</button>
    </c-form>
  </div>
</template>

<script>
  import CForm from '@/components/CForm'
  import CFormItem from '@/components/CFormItem'
  import CInput from '@/components/CInput'

  export default {
    name: 'app',
    data() {
      return {
        ruleForm: {
          name: '',
          password: ''
        },
        rules: {
          name: [{ required: true, message: '请输入用户名', trigger: 'change' }],
          password: [{ required: true, message: '请输入密码', trigger: 'change' }]
        }
      }
    },
    components: { CForm, CFormItem, CInput },
    methods: {
      submit(formName) {
        this.$refs[formName].validate((valid) => {
          if (valid) {
            console.log('submit!')
          } else {
            console.log('error submit!!')
            return false
          }
        })
      }
    }
  }
</script>

<style>
  #app {
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
  }
</style>
