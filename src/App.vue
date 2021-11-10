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
      sampleData: 'hello',
    };
  },
  created() {
    this.listenMsg();
  },
  methods: {
    listenMsg() {
      const domains = [
        "http://localhost:3000",
        "https://sit-portal.the1.co.th",
        "https://uat-portal.the1.co.th",
        "https://pvt-portal.the1.co.th",
        "https://portal.the1.co.th",
      ];

      console.log("start listen v.7 : ");
      let tempIns = this

      console.log("tempins : ", tempIns.sampleData)
      //respond to events
      window.addEventListener(
        "message",
        function (event) {
          console.log("debug : ", event);

          // if (event.origin !== "http://localhost:3000") return;
          if (domains.indexOf(event.origin) === -1) return;

          console.log("message received:  " + event.data, event);

          tempIns.sampleData(JSON.parse(event.data));
          sessionStorage.setItem("renderJson", event.data);

          event.source.postMessage("i get it!", event.origin);
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
