<template>
  <div class="about">
    <h1>这是input组件</h1>
    <v-input
      v-model="msg"
      type="textarea"
      clearable
      placeholder="请输入"
    ></v-input>
    <v-input v-model="msg3" placeholder="请输入" clearable></v-input>

    <!-- <input type="text" v-model="msg" /> -->
    <div>{{ msg }}</div>
    <div>{{ msg3 }}</div>
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
      msg3: ''
    }
  },
  methods: {},
  components: {
    vInput
  }
}
</script>
