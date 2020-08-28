<template>
  <div>
    <slot></slot>
  </div>
</template>

<script>
export default {
  props: {
    rules: Object,
  },
  provide() {
    return {
      rules: this.rules,
    }
  },
  methods: {
    validateFields() {},
  },
}
</script>

<style></style>
