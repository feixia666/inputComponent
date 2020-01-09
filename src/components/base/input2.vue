<template>
  <div class="main" :style="`width: ${width}px;height: ${height}px`">
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
    // input框类型
    type: {
      type: String,
      default: 'text'
    },
    // input框尺寸
    size: {
      type: String,
      default: 'medium'
    },
    // 文本提示
    placeholder: {
      type: String,
      default: null
    },
    // 是否可输入
    disabled: {
      type: Boolean,
      default: false
    },
    // 是否可一键清除
    clearable: {
      type: Boolean,
      default: false
    },
    areasize: {
      type: Object,
      default: function() {
        return {
          cols: 30,
          rows: 5
        }
      }
    }
  },
  computed: {
    // 实现父子组件双向数据绑定
    newValue: {
      get() {
        return this.value
      },
      set: function(value) {
        return this.$emit('input', value)
      }
    }
  },
  created() {
    // eslint-disable-next-line no-console
    this.setSize()
  },
  data() {
    return {
      width: 120,
      height: 30
    }
  },
  methods: {
    // 清空
    cleanAll() {
      this.newValue = ''
    },
    // 父组件chang事件，仅在输入框失去焦点或用户按下回车时触发，父组件调用时通过$event获取值
    setValue() {
      this.$emit('change', this.value)
    },
    // 根据父组件传的size，设置input框尺寸
    setSize() {
      if (this.size == 'medium') {
        this.width = 120
        this.height = 30
      } else if (this.size == 'mini') {
        this.width = 80
        this.height = 20
      } else if (this.size == 'large') {
        this.width = 150
        this.height = 40
      } else if (this.size == 'small') {
        this.width = 100
        this.height = 25
      }
    }
  }
}
</script>

<style lang="scss" scoped>
.main {
  position: relative;
  display: inline-block;
  width: 180px;
  height: 50px;
  margin: 5px;
  .input-area {
    width: 100%;
    height: 100%;
    padding: 5px;
    box-sizing: border-box;
    padding-right: 23px;
  }
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
    right: 6px;
    top: 50%;
    margin-top: -7px;
    color: #b4bccc;
  }
  .textarea {
  }
}
</style>
