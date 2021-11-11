<template>
  <img alt="Vue logo" src="./assets/logo.png" />
  <HelloWorld msg="Welcome to Your Vue.js App" :sampleData="sampleData" />
</template>

<script>
import HelloWorld from "./components/HelloWorld.vue";

export default {
  name: "App",
  components: {
    HelloWorld,
  },
  data() {
    return {
      sampleData: "hello",
    };
  },
  created() {
    this.listenMsg();
  },
  methods: {
    listenMsg() {
      const domains = [
        "http://localhost:3000",
        "http://localhost:3000/dropLead",
        "https://sit-portal.the1.co.th",
        "https://uat-portal.the1.co.th",
        "https://pvt-portal.the1.co.th",
        "https://portal.the1.co.th",
      ];

      console.log("start listen v.11 : ");
      let tempIns = this;

      console.log("tempins : ", tempIns.sampleData);
      //respond to events
      window.addEventListener(
        "message",
        function (event) {
          if (event.data.originName && event.data.originName === "the1portal") {
            let { originName, value } = event.data;
            console.log("originName : ", originName);
            console.log("debug : ", event);
            // if (event.origin !== "http://localhost:3000") return;
            if (domains.indexOf(event.origin) === -1) return;
            console.log("message received:  " + value, event);

            tempIns.sampleData = JSON.parse(value);
            sessionStorage.setItem("renderJson", value);
            event.source.postMessage("i get it!", event.origin);
          }
        },
        false
      );
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
