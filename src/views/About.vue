<template>
  <div class="about">
    <h1>这是input组件</h1>
    <v-input
      v-model="msg"
      type="text"
      size="mini"
      clearable
      prefix-icon="icon-mianbao"
      placeholder="请输入"
    ></v-input>
    <v-input
      v-model="msg1"
      placeholder="请输入"
      clearable
      prefix-icon="icon-bobantang"
      suffix-icon="icon-tiantong"
      size="small"
    ></v-input>
    <v-input
      @change="getValue($event)"
      v-model="msg2"
      suffix-icon="icon-luobu"
    ></v-input>
    <v-input size="large" v-model="msg3"></v-input>
    <!-- <input type="text" v-model="msg" /> -->

    <br />
    <v-input v-model="msg4">
      <template v-slot:prepend>Http://</template>
    </v-input>
    <v-input v-model="msg6">
      <template v-slot:append>.com</template>
    </v-input>
    <br />
    <v-input v-model="msg5">
      <template v-slot:prepend>Http://</template>
      <template v-slot:append>.com</template>
    </v-input>
    <br />
    <v-input type="textarea"></v-input>
    <!-- <v-input
      ><template v-slot:hh="aa">
        {{ aa.mgr }}
      </template></v-input
    > -->
    <div>{{ msg }}</div>
    <div>{{ msg1 }}</div>
    <div>{{ msg2 }}</div>
    <div>{{ msg3 }}</div>
    <div>{{ msg4 }}</div>
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
      msg4: '',
      msg5: '',
      msg6: '',
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
