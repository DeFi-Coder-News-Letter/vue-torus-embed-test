<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png" />
    <button @click="login">Login</button>
  </div>
</template>

<script>
import Torus from "@toruslabs/torus-embed";
import Web3 from "web3";

export default {
  name: "app",
  methods: {
    async login() {
      try {
        const torus = new Torus();
        window.torus = torus;
        await torus.init("development");
        await torus.ethereum.enable();
        const web3 = new Web3(torus.provider);
        web3.eth.getAccounts().then(accounts => {
          web3.eth.getBalance(accounts[0]).then(console.log)
        });
      } catch (error) {
        console.error(error);
      }
    }
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
