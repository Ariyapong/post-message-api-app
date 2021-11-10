<template>
  <img alt="Vue logo" src="./assets/logo.png" />
  <HelloWorld msg="Welcome to Your Vue.js App" />
</template>

<script>
import HelloWorld from "./components/HelloWorld.vue";

export default {
  name: "App",
  components: {
    HelloWorld,
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
        "https://portal.the1.co.th"
      ];

      console.log("start listen : ");
      //respond to events
      window.addEventListener(
        "message",
        function (event) {
          console.log("debug : ", event);
          // if (event.origin !== "http://localhost:3000") return;
          if (domains.indexOf(event.origin) === -1) return;
          console.log("message received:  " + event.data, event);
          event.source.postMessage("holla back youngin!", event.origin);
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
