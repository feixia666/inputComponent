<template>
  <div class="about">
    <h1>这是input组件</h1>
    <v-input
      v-model="msg"
      type="text"
      size="large"
      clearable
      placeholder="请输入"
    ></v-input>
    <v-input
      v-model="msg3"
      placeholder="请输入"
      clearable
      size="mini"
    ></v-input>
    <v-input @change="getValue($event)" v-model="msg2"></v-input>
    <!-- <input type="text" v-model="msg" /> -->
    <div>{{ msg }}</div>
    <div>{{ msg3 }}</div>
    <div>{{ msg2 }}</div>
  </div>
</template>

<script>
import vInput from '../components/base/input2'
export default {
  data() {
    return {
      msg: '',
      msg1: '',
      msg2: '',
      msg3: '',
      areasize: { cols: 50, rows: 5 }
    }
  },
  methods: {
    getValue(val) {
      // eslint-disable-next-line no-console
      console.log(val)
    }
  },
  components: {
    vInput
  }
}
</script>
