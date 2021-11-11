<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png" />
    <HelloWorld msg="Calculator" />
    <div class="display">
      <input
        type="number"
        placeholder="Input operand1"
        v-model.number="operand1"
      />
      <input
        type="number"
        placeholder="Input operand2"
        v-model.number="operand2"
      />
      <br />
      Result: {{ result }}
    </div>
    <div class="keyboard">
      <button @click="onPlus">+</button>
      <button @click="onMinus">-</button>
      <button :disabled="operand2 == 0" @click="onDiv">/</button>
      <button @click="onMul">*</button>
      <button @click="onElevate">Elevate</button>
      <button @click="onRemainder">Remainder</button>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from "@/components/HelloWorld.vue";

export default {
  name: "Calculator",
  data() {
    return {
      operand1: 0,
      operand2: 0,
      result: 0,
    };
  },
  methods: {
    onPlus() {
      this.result = this.operand1 + this.operand2;
    },
    onMinus() {
      this.result = this.operand1 - this.operand2;
    },

    onMul() {
      this.result = this.operand1 * this.operand2;
    },

    onDiv() {
      this.result = this.operand1 / this.operand2;
    },
    onElevate() {
      this.result = this.operand1 ** this.operand2;
    },
    onRemainder() {
      this.result = this.operand1 % this.operand2;
    },
  },
  components: {
    HelloWorld,
  },
};
</script>