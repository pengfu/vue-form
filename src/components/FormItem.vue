<template>
  <div>
    <label>{{ label }}</label>
    <slot> </slot>
    <div v-if="errMessage">{{ errMessage }}</div>
  </div>
</template>

<script>
import Schema from 'async-validator'
export default {
  inject: ['rules'],
  props: {
    label: String,
    prop: String,
  },
  created() {
    this.$on('validate', (val) => {
      this.validate(val)
    })
  },
  data() {
    return {
      errMessage: '',
    }
  },
  methods: {
    validate(val) {
      //   alert('validate !')

      const des = {[this.prop]:this.rules[this.prop][0]}
      console.log(des)
      const validator = new Schema(des)
      validator.validate({ [this.prop]: val }, (errors, fields) => {
        if (errors) {
          // validation failed, errors is an array of all errors
          // fields is an object keyed by field name with an array of
          // errors per field
          //   return handleErrors(errors, fields)
          console.log(errors, fields)
          this.errMessage = '错误'
        } else {
          this.errMessage = ''
        }
        // validation passed
      })
    },
  },
}
</script>

<style></style>
