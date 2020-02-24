<template>
  <div class="container d-flex justify-content-center">
    <div class="row">
      <h3 class="col">Bin2Dec Converter</h3>
      <input class="col" type="text" v-model="inputNum" />
      <h3 class="col">
        <animated-number
          :value="parseInt(Number(inputNum), 2)"
          :duration="900"
        ></animated-number>
      </h3>
    </div>
  </div>
</template>

<script>
import AnimatedNumber from "animated-number-vue";

export default {
  components: {
    AnimatedNumber
  },
  data() {
    return {
      inputNum: ""
    };
  },
  computed: {
    binaryToDecimal() {
      return parseInt(this.inputNum, 2).toFixed(2);
    }
  },
  methods: {
    getEndStr(string) {
      let end = string
        .split("")
        .splice(string.length - 1, string.length)
        .join("");
      if (end === "0" || end === "1") {
        return;
      } else {
        this.deleteUnwanted(string);
      }
    },
    deleteUnwanted(string) {
      let newString = string
        .split("")
        .slice(0, string.length - 1)
        .join("");
      this.inputNum = newString;
    },
    checkStringLen(string) {
      if (string.length > 8) {
        let newStr = string
          .split("")
          .slice(0, -1)
          .join("");
        this.inputNum = newStr;
      } else {
        return;
      }
    }
  },
  updated() {
    console.log(this.inputNum);
    this.getEndStr(this.inputNum);
    this.checkStringLen(this.inputNum);
  }
};
</script>

<style>
.container {
  min-height: 100%;
  min-height: 100vh;

  display: flex;
  align-items: center;
}
</style>
