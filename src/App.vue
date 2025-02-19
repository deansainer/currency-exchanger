<script>
import Input from './components/input.vue';
import Selector from './components/Selector.vue'
import CryptoConvert from 'crypto-convert';

const convert = new CryptoConvert();

export default{
  components: {Input, Selector},

  data(){
    return{
      amount: 0,
      cryptoFirst: '',
      cryptoSecond: '',
      error: '',
      result: 0
    }
  },
  methods: {
    setAmount(val){
      this.amount = val
      console.log(this.amount)
    },

    setCryptoFirst(val){
      this.cryptoFirst = val
    },

    setCryptoSecond(val){
      this.cryptoSecond = val
    },
    async convert(){
      if(this.amount < 1){
        this.error = 'Enter a number more that 0'
        return;
      } else if (this.cryptoFirst === this.cryptoSecond){
        this.error = 'Choose different currencies '
        return;
      } else if (this.cryptoFirst == '' || this.cryptoSecond == ''){
        this.error = 'Choose 2 currencies '
        return;
      }
      this.error = ''

      await convert.ready()
      if(this.cryptoFirst == 'BTC' && this.cryptoSecond == 'ETH'){
        this.result = convert.BTC.ETH(this.amount)
      } else if (this.cryptoFirst == 'BTC' && this.cryptoSecond == 'USDT'){
        this.result = convert.BTC.USDT(this.amount)
      } else if (this.cryptoFirst == 'ETH' && this.cryptoSecond == 'BTC'){
        this.result = convert.ETH.BTC(this.amount)
      } else if (this.cryptoFirst == 'ETH' && this.cryptoSecond == 'USDT'){
        this.result = convert.ETH.USDT(this.amount)
      } else if (this.cryptoFirst == 'USDT' && this.cryptoSecond == 'BTC'){
        this.result = convert.USDT.BTC(this.amount)
      } else if (this.cryptoFirst == 'USDT' && this.cryptoSecond == 'ETH'){
        this.result = convert.USDT.ETH(this.amount)
      }
      
    }

  }
}
</script>

<template>
  <p v-if="error != ''">{{ error }}</p>
  <p v-if="result != 0">{{ result }}</p>
  <h1>Crypto exchanger</h1>
  <Input :setAmount="setAmount" :convert="convert"/> 
  <div className="selectors">
    <Selector :setCrypto="setCryptoFirst"/>
    <Selector :setCrypto="setCryptoSecond"/>
  </div>
{{ amount }}
</template>

<style>

</style>
