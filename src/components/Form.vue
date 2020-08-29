<template>
  <div>
    <slot></slot>
  </div>
</template>

<script>
export default {
  props: {
    rules: Object,
    model: Object,
  },
  provide() {
    return {
      rules: this.rules,
      model: this.model,
    }
  },
  methods: {
    validateFields(cb) {
      let tasks = this.$children
        .filter((item) => item.prop)
        .map((it) => it.validate())
      console.log('tasks', tasks)

      Promise.all(tasks)
        .then((result) => {
          console.log('result', result)
          //   处理错误结果
          let err = result.filter((it) => it)
          if (err.length > 0) {
            cb(err)
          } else {
            cb('')
          }
        })
        .catch((err) => {
          cb(err)
        })
    },
  },
}
</script>

<style></style>
