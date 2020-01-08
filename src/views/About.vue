<template>
  <div class="about">
    <h1>这是input组件</h1>
    <v-input v-model="msg" placeholder="ashhh"></v-input>
    <v-input v-model="msg1" :disabled="true"></v-input>
    <dy-input v-model="msg2"></dy-input>
    <!-- <input type="text" v-model="msg" /> -->
    <div>{{ msg }}</div>
    <div>{{ msg1 }}</div>
    <div>{{ msg2 }}</div>
  </div>
</template>

<script>
import vInput from '../components/base/input'
import dyInput from '../components/base/input2'
export default {
  data() {
    return {
      msg: '',
      msg1: '',
      msg2: ''
    }
  },
  methods: {},
  components: {
    vInput,
    dyInput
  }
}
</script>
