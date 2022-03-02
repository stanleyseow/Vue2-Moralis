<template>
  <div id="app"></div>
</template>

<script>
import Moralis from "moralis";
const serverUrl = process.env.VUE_APP_MORALIS_SERVER_URL;
const appId = process.env.VUE_APP_MORALIS_APPLICATION_ID;
//const contractAddress = "0x77737d90458ef4b0D5253342bD22ceEC406Eba80";
export default {
  name: "App",
  components: {},
  data() {
    return {};
  },
  methods: {},
  computed: {},
  watch: {},
  mounted() {
    Moralis.start({ serverUrl, appId });
    window.Moralis = Moralis;
  },
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
}
</style>
