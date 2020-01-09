<template>
  <div class="main" :style="`width: ${width}px;height: ${height}px`">
    <template v-if="type == 'text'">
      <span v-if="prefixIcon" class="prefix-icon">
        <i :class="`iconfont ${prefixIcon}`"></i>
      </span>
      <input
        class="input-area"
        type="text"
        v-model="newValue"
        :placeholder="placeholder"
        :disabled="disabled"
        @blur="setValue"
        @keyup.enter="setValue"
        :style="
          `padding-left: ${pdl}px;padding-right: ${pdr}px;font-size: ${fs}px;`
        "
      />
      <span
        class="clean"
        @click="cleanAll"
        v-if="clearable"
        v-show="newValue != ''"
        :style="`right: ${mgr}px`"
        >x</span
      >
      <span v-if="suffixIcon" class="suffix-icon">
        <i :class="`iconfont ${suffixIcon}`"></i>
      </span>
      <div v-if="existPrepend" class="prepend">
        <slot name="prepend"></slot>
      </div>
      <div v-if="existAppend" class="append">
        <slot name="append"></slot>
      </div>
      <slot v-bind:mgr="width" name="hh"></slot>
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
    },
    prefixIcon: {
      type: String,
      default: null
    },
    suffixIcon: {
      type: String,
      default: null
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
  mounted() {
    // eslint-disable-next-line no-console
    if (this.$slots.prepend && this.$slots.prepend.length > 0) {
      this.existPrepend = true
      this.width = 320
      this.pdl = 85
    }
    if (this.$slots.append && this.$slots.append.length > 0) {
      this.existAppend = true
      this.width = 320
      this.pdr = 85
    }
    this.setSize()
    this.setTextPadding()
  },
  data() {
    return {
      width: 120,
      height: 35,
      pdl: null,
      pdr: null,
      fs: 14,
      mgr: 6,
      existPrepend: false,
      existAppend: false
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
      if (!this.existPrepend && !this.existAppend) {
        if (this.size == 'medium') {
          this.width = 160
          this.height = 35
          this.fs = 16
        } else if (this.size == 'mini') {
          this.width = 120
          this.height = 25
        } else if (this.size == 'large') {
          this.width = 180
          this.height = 40
          this.fs = 20
        } else if (this.size == 'small') {
          this.width = 140
          this.height = 30
        }
      }
    },
    setTextPadding() {
      // eslint-disable-next-line no-console
      if (this.prefixIcon != null) {
        this.pdl = 18
      }
      if (this.suffixIcon != null) {
        this.pdr = 23
      }
      if (this.clearable) {
        // eslint-disable-next-line no-console
        this.pdr = 23
        this.mgr = 6
      }
      if (this.suffixIcon != null && this.clearable) {
        this.pdr = 40
        this.mgr = 25
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
  height: 35px;
  margin: 5px;
  .prefix-icon {
    display: inline-block;
    font-size: 12px;
    width: 12px;
    height: 12px;
    line-height: 12px;
    position: absolute;
    left: 3px;
    top: 50%;
    margin-top: -7px;
  }
  .input-area {
    width: 100%;
    height: 100%;
    padding: 5px;
    box-sizing: border-box;
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
    top: 50%;
    margin-top: -7px;
    color: #b4bccc;
  }
  .suffix-icon {
    display: inline-block;
    font-size: 12px;
    width: 12px;
    height: 12px;
    line-height: 12px;
    position: absolute;
    top: 50%;
    right: 10px;
    margin-top: -7px;
  }
  .prepend {
    display: inline-block;
    width: 80px;
    height: 100%;
    line-height: 35px;
    box-sizing: border-box;
    border: 1px solid #909399;
    color: #909399;
    background-color: #f5f7fa;
    position: absolute;
    top: 0;
    left: 0;
  }
  .append {
    display: inline-block;
    width: 80px;
    height: 100%;
    line-height: 35px;
    box-sizing: border-box;
    border: 1px solid #909399;
    color: #909399;
    background-color: #f5f7fa;
    position: absolute;
    top: 0;
    right: 0;
  }
}
</style>
