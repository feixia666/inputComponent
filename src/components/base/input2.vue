<template>
  <div>
    <input type="text" :value="value" @input="update" />
  </div>
</template>

<script>
export default {
  props: {
    value: {
      type: String,
      value: ''
    }
  },
  data() {
    return {
      show: ''
    }
  },

  methods: {
    update(val) {
      this.$emit('input', val)
    }
  }
}
</script>
