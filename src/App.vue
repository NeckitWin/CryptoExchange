<script>
import Input from "@/components/Input.vue";
import Selector from "@/components/Selector.vue";
import CryptoConvert from "crypto-convert";

const convert = new CryptoConvert()

export default {
  components: {Input, Selector},

  data() {
    return {
      amount: 0,
      cryptoFirst: '',
      cryptoSecond: '',
      error: '',
      result: 0
    }
  },
  methods: {
    changeAmount(val) {
      this.amount = val
    },
    setCryptoFirst(val) {
      this.cryptoFirst = val
    },
    setCryptoSecond(val) {
      this.cryptoSecond = val
    },
    async convert() {
      if (this.amount <= 0) {
        this.error = 'Enter a number greater than 0!'
        return
      } else if (this.cryptoFirst == '' || this.cryptoSecond == '') {
        this.error = 'Choose a currency'
        return
      } else if (this.cryptoFirst == this.cryptoSecond) {
        this.error = 'Select different currency types!'
        return
      }
      this.error = ''

      await convert.ready()

      if (this.cryptoFirst == 'BTC' && this.cryptoSecond == 'ETH') {
        this.result = convert.BTC.ETH(this.amount)
      } else if (this.cryptoFirst == 'BTC' && this.cryptoSecond == 'USDT') {
        this.result = convert.BTC.USDT(this.amount)
      } else if (this.cryptoFirst == 'ETH' && this.cryptoSecond == 'BTC') {
        this.result = convert.ETH.BTC(this.amount)
      } else if (this.cryptoFirst == 'ETH' && this.cryptoSecond == 'USDT') {
        this.result = convert.ETH.USDT(this.amount)
      } else if (this.cryptoFirst == 'USDT' && this.cryptoSecond == 'BTC') {
        this.result = convert.USDT.BTC(this.amount)
      } else if (this.cryptoFirst == 'USDT' && this.cryptoSecond == 'ETH') {
        this.result = convert.USDT.ETH(this.amount)
      }
    }
  }
}
</script>

<template>
  <h1>Crypto exchange</h1>
  <Input :changeAmount="changeAmount" :convert="convert" :error="error"/>
  <p v-if="result != 0">{{ result }} {{ cryptoSecond }}</p>
  <div class="selectors">
    <Selector :setCrypto="setCryptoFirst"/>
    <Selector :setCrypto="setCryptoSecond"/>
  </div>
</template>

<style scoped>
.selectors {
  display: flex;
  justify-content: space-around;
  width: 700px;
  margin: 0 auto;
}

p{
  font-size: 2em;
  color: #FFFFFF;
}
</style>
