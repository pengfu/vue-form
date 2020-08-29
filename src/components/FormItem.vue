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
  inject: ['rules', 'model'],
  props: {
    label: String,
    prop: String,
  },
  created() {
    this.$on('validate', () => {
      this.validate(this.model[this.prop])
    })
  },
  data() {
    return {
      errMessage: '',
    }
  },
  methods: {
    validate() {
      const val = this.model[this.prop]
      const des = { [this.prop]: this.rules[this.prop] }
      const validator = new Schema(des)
      return new Promise((resolve) => {
        validator.validate({ [this.prop]: val }, (errors) => {
          if (errors) {
            // validation failed, errors is an array of all errors
            // fields is an object keyed by field name with an array of
            // errors per field
            this.errMessage = errors.find(
              (item) => item.field === this.prop
            ).message
            resolve(errors)
          } else {
            this.errMessage = ''
            resolve('')
          }
        })
      })
    },
  },
}
</script>

<style></style>
