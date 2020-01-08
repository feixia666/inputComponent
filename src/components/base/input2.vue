<template>
  <div class="main">
    <template v-if="type == 'text'">
      <input
        class="input-area"
        type="text"
        v-model="newValue"
        :placeholder="placeholder"
        :disabled="disabled"
        @blur="setValue"
        @keyup.enter="setValue"
      />
      <span
        class="clean"
        @click="cleanAll"
        v-if="clearable"
        v-show="newValue != ''"
        >x</span
      >
    </template>
    <template v-if="type == 'textarea'">
      <textarea
        class="textarea"
        :cols="areasize.cols"
        :rows="areasize.rows"
        v-model="newValue"
        :placeholder="placeholder"
        :disabled="disabled"
      ></textarea>
      <span
        class="clean"
        @click="cleanAll"
        v-if="clearable"
        v-show="newValue != ''"
        >x</span
      >
    </template>
  </div>
</template>

<script>
export default {
  props: {
    value: {
      type: String,
      value: ''
    },
    type: {
      type: String,
      default: 'text'
    },
    placeholder: {
      type: String,
      default: null
    },
    disabled: {
      type: Boolean,
      default: false
    },
    clearable: {
      type: Boolean,
      default: false
    }
  },
  computed: {
    newValue: {
      get() {
        return this.value
      },
      set: function(value) {
        return this.$emit('input', value)
      }
    }
  },
  data() {
    return {
      areasize: {
        cols: 20,
        rows: 2
      }
    }
  },
  methods: {
    cleanAll() {
      this.newValue = ''
    },
    setValue() {
      this.$emit('change', this.value)
    }
  }
}
</script>

<style lang="scss" scoped>
.main {
  position: relative;
  .clean {
    display: inline-block;
    font-size: 12px;
    width: 12px;
    height: 12px;
    line-height: 12px;
    border: 1px solid #b4bccc;
    border-radius: 50%;
    cursor: pointer;
    position: absolute;
    left: 500px;
    top: 50%;
    margin-top: -6px;
    color: #b4bccc;
  }
  .textarea {
  }
}
</style>
