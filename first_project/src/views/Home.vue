<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png" />
    <HelloWorld msg="Calculator" />
    <div class="display">
      <input
        type="number"
        placeholder="Input Operand 1"
        v-model.number="operand1"
      />
      <input
        type="number"
        placeholder="Input Operand 2"
        v-model.number="operand2"
      />
      <br />
      <span>Result: {{ result }}</span>
    </div>
    <div class="keyboard">
      <button
        v-for="operand in operands"
        v-bind:key="operand"
        v-bind:disabled="operand1 === '' || operand2 === ''"
        @click="calculate(operand)"
      >
        {{ operand }}
      </button>
      <br />
      <input type="checkbox" id="checkbox" v-model="checked" />
      <span>Show keyboard</span>
      <div class="keyboard" v-show="checked">
        <button
          v-for="number in numbers"
          v-bind:key="number"
          @click="numberInput(number)"
        >
          {{ number }}
        </button>
        <br />
        <input type="radio" name="field" id="one" value="one" v-model="field" />
        <label for="one">Operand 1</label>
        <input type="radio" name="field" id="two" value="two" v-model="field" />
        <label for="two">Operand 2</label>
      </div>
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
      operand1: "",
      operand2: "",
      result: 0,
      operands: ["+", "-", "/", "*", "**", "%", "C"],
      numbers: [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, "Back"],
      checked: false,
      field: "one",
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
      if (this.operand2 === 0) {
        this.result = "You cannot divide by 0 !!!";
      } else {
        this.result = this.operand1 / this.operand2;
      }
    },

    onElevate() {
      this.result = this.operand1 ** this.operand2;
    },

    onRemainder() {
      if (this.operand2 === 0) {
        this.result = "You cannot divide by 0 !!!";
      } else {
        this.result = this.operand1 % this.operand2;
      }
    },

    onClear() {
      this.operand1 = "";
      this.operand2 = "";
      this.result = 0;
    },

    calculate(operation = "+") {
      this.operand1 = Number(this.operand1);
      this.operand2 = Number(this.operand2);
      switch (operation) {
        case "+":
          this.onPlus();
          break;
        case "-":
          this.onMinus();
          break;
        case "*":
          this.onMul();
          break;
        case "/":
          this.onDiv();
          break;
        case "**":
          this.onElevate();
          break;
        case "%":
          this.onRemainder();
          break;
        case "C":
          this.onClear();
          break;
      }
    },

    numberInput(addNumber) {
      if (this.field === "one") {
        if (addNumber === "Back") {
          this.operand1 = String(this.operand1);
          return (this.operand1 = this.operand1.slice(0, -1));
        }
        this.operand1 = `${this.operand1}${addNumber}`;
      } else {
        if (addNumber === "Back") {
          this.operand2 = String(this.operand2);
          return (this.operand2 = this.operand2.slice(0, -1));
        }
        this.operand2 = `${this.operand2}${addNumber}`;
      }
    },
  },
  components: {
    HelloWorld,
  },
};
</script>