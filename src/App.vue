<template>
  <div id="app" class="mx-2 my-2">
    <input v-model="walletAddress" placeholder="Wallet Address" />
    <button @click="walletQuery(walletAddress)">Submit</button> <br />

    <br />
    ERC-20 contract :<b>{{ this.contractAddress }}</b>  <br />
    Name: <b>{{ metaData.name }}</b> <br />
    Symbol : <b>{{ metaData.symbol }}</b> <br />
    <br/>

    User Wallet : {{walletAddress}} <br/>
    <div v-for="item in walletBalance" :key="item.name">
      Name : {{ item.name}} <br/>
      SYM: {{ item.symbol}} <br/>
      Balance: {{ item.balance}} <br/>
    </div>

  </div>
</template>

<script>
import Moralis from "moralis";
const serverUrl = process.env.VUE_APP_MORALIS_SERVER_URL;
const appId = process.env.VUE_APP_MORALIS_APPLICATION_ID;
export default {
  name: "App",
  components: {},
  data() {
    return {
      walletAddress: "",
      metaData: {},
      contractAddress: "0x77737d90458ef4b0D5253342bD22ceEC406Eba80",
      walletBalance: []
    };
  },
  methods: {
    async walletQuery(data) {
      console.log("walletQuery");
      this.walletAddress = data;

      let options = {
        chain: "0x4",
        addresses: this.contractAddress,
      };

      this.metaData = await Moralis.Web3API.token.getTokenMetadata(options);
      console.log("metadata: ", this.metaData);
      this.metaData.name = this.metaData[0].name
      this.metaData.symbol = this.metaData[0].symbol

      let option2 = {
        chain: "0x4",
        address : this.walletAddress
      }
      this.walletBalance = await Moralis.Web3API.account.getTokenBalances(option2);
      console.log("Wallet Balance: ",this.walletBalance )


    },
  },
  computed: {},
  watch: {},
  async mounted() {
    Moralis.start({ serverUrl, appId });
    window.Moralis = Moralis;
    await Moralis.enableWeb3();
  },
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
}
</style>
