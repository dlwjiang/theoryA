<template>

  <div id="clash-container">

    <div id="bars" v-if="yesValue && noValue">
      <span class="yes bar" :style="yesStyle" @click="open(`https://etherscan.io/address/${yesAddress}`)">
        yes <span class="value">({{yesValue}} eth)</span>
      </span>
      <span class="no bar" :style="noStyle" @click="open(`https://etherscan.io/address/${noAddress}`)">
        <a :href="`https://etherscan.io/address/${noAddress}`" target="_blank">
          no <span class="value">({{noValue}} eth)</span>
        </a>
      </span>
    </div>

    <div v-else id="error">
      <div>API is probably overloaded</div>
      <div>
        Yes:
        <a :href="`https://etherscan.io/address/${yesAddress}`" target="_blank">
          {{yesAddress}}
        </a>
      </div>
      <div>
        No:
        <a :href="`https://etherscan.io/address/${noAddress}`" target="_blank">
          {{noAddress}}
        </a>
      </div>
    </div>

    <div id="powered-by">bars adjust based on wallet value. powered by <a href="https://ethplorer.io/" target="_blank">ethplorer.io</a></div>

  </div>

</template>

<script>

  export default {
    name: 'clashOfFaith',
    data: function () {
      return {
        yesValue   : null,
        noValue    : null,
        yesAddress : '0xf35fff8e612af8d66367313ffc0677930252a370',
        noAddress  : '0x26bee4879a24762576add92d64466f333f33d39f'
      }
    },
    mounted: function () {
      const yesUrl     = `https://api.ethplorer.io/getAddressInfo/${this.yesAddress}?apiKey=freekey`;
      const noUrl      = `https://api.ethplorer.io/getAddressInfo/${this.noAddress}?apiKey=freekey`;
      fetch(yesUrl)
      .then(response => response.json())
      .then(data => {
        this.yesValue = data.ETH.balance;
      })
      fetch(noUrl)
      .then(response => response.json())
      .then(data => {
        this.noValue = data.ETH.balance;
      })
    },
    computed: {
      yesStyle: function () {
        return {
          'flex-grow': this.yesValue
        }
      },
      noStyle: function () {
        return {
          'flex-grow': this.noValue
        }
      }
    },
    methods: {
      open: function (url) {
        window.open(url);
      }
    }

  }

</script>

<style lang="less" scoped>

  #clash-container {
    margin-bottom: 10px;
    #bars {
      display: flex;
      .bar {
        cursor: pointer;
        display: inline-block;
        height: 20px;
        text-align: center;
        color: white;
        padding: 4px;
        a {
          color: white;
          text-decoration: none;
        }
        .value {
          font-size: 12px;
        }
      }
      .yes {
        background-color: gold;
        border-top-left-radius: 5px;
        border-bottom-left-radius: 5px;
      }
      .no {
        background-color: maroon;
        border-top-right-radius: 5px;
        border-bottom-right-radius: 5px;
      }
      .yes.bar:hover {
        background-color: darken(gold, 5%);
      }
      .no.bar:hover {
        background-color: lighten(maroon, 5%);
      }
    }
    #error {
      border: 1px solid grey;
      border-radius: 5px;
      padding: 5px 10px;
    }
    #powered-by {
      text-align: right;
      font-size: 10px;
      margin-top: 2px;
      color: grey;
      a {
        color: grey;
      }
    }
  }

</style>