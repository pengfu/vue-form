<template>
  <div id="app">
    
    <Form :model="user" :rules="rules" ref="loginForm">
      <FormItem label="用户名" prop="userName">
        <Input v-model="user.userName" />
      </FormItem>
      <FormItem label="密码" prop="password">
        <Input v-model="user.password" type="password" />
      </FormItem>
      <FormItem>
        <button @click="submit">登录</button>
      </FormItem>
    </Form>
    {{ user }}
  </div>
</template>

<script>
import Form from './components/Form'
import FormItem from './components/FormItem'
import Input from './components/Input'

export default {
  name: 'App',
  data() {
    return {
      user: {
        userName: 'zhangsan',
        password: 'abc123',
      },
      rules: {
        userName: { required: true },
        password: { required: true },
      },
    }
  },
  methods: {
    submit() {
      this.$refs.loginForm.validateFields((err) => {
        if (!err) {
          alert('执行登录')
        } else {
          alert(`有错: ${JSON.stringify(err)}`)
        }
      })
    },
  },
  components: {
    Form,
    FormItem,
    Input,
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
