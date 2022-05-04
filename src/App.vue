<template>
  <input type="text" v-model="firstText" />
  <input type="text" v-model="secondText" />
  <button @click="showText">Submit</button>
  <HelloWorld :combined-text="combinedText" />
</template>

<script>
import HelloWorldVue from "./components/HelloWorld.vue";
export default {
  name: "App",
  components: {
    HelloWorld: HelloWorldVue,
  },
  data() {
    return {
      firstText: "",
      secondText: "",
      // combinedText: "",
    };
  },
  computed: {
    combinedText() {
      return this.firstText + this.secondText;
    },
  },
  watch: {
    firstText(newValue, oldValue) {
      if (newValue !== oldValue && newValue.length > oldValue.length) {
        let pattern = new RegExp(/^[A-Z]+$/i);
        if (!pattern.test(newValue)) {
          this.showError();
          this.firstText = oldValue;
        }
      }
    },
    secondText: function (newValue, oldValue) {
      if (newValue !== oldValue && newValue.length > oldValue.length) {
        let pattern = new RegExp(/^[A-Z]+$/i);
        if (!pattern.test(newValue)) this.showError();
      }
    },
  },
  methods: {
    showText() {
      this.combinedText = this.firstText + this.secondText;
    },
    showError() {
      alert("only enter alphabet");
    },
  },
};
</script>

<style>
</style>
