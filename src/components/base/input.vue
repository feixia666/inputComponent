<template>
  <div>
    <input
      type="text"
      v-model="show"
      :placeholder="placeholder"
      :disabled="disabled"
    />
  </div>
</template>

<script>
export default {
  props: {
    value: {
      type: String,
      default: ''
    },
    placeholder: {
      type: String,
      default: null
    },
    disabled: {
      type: Boolean,
      default: false
    }
  },
  data() {
    return {
      show: ''
    }
  },
  watch: {
    value(val) {
      if (val === this.show) {
        return ''
      }

      this.show = val
    },
    show(val) {
      this.$emit('input', val)
    }
  },
  methods: {}
}
</script>
