<script>
import Favorites from './components/Favorites.vue';
import Input from './components/input.vue';
import Selector from './components/Selector.vue'
import CryptoConvert from 'crypto-convert';

const convert = new CryptoConvert();

export default{
  components: {Input, Selector, Favorites},

  data(){
    return{
      amount: 0,
      cryptoFirst: '',
      cryptoSecond: '',
      error: '',
      result: 0,
      favorites: []
    }
  },
  methods: {
    setAmount(val){
      this.amount = val
      this.result = 0
    },

    setCryptoFirst(val){
      this.cryptoFirst = val
      this.result = 0
    },

    setCryptoSecond(val){
      this.cryptoSecond = val
      this.result = 0
    },

    toFavorite(){
      this.favorites.push({
        from: this.cryptoFirst,
        to: this.cryptoSecond
      })
      console.log(this.favorites)
    },

    async convert(){
      if(this.amount < 1){
        alert('Enter a number more that 0')
        return;
      } else if (this.cryptoFirst === this.cryptoSecond){
        alert('Choose different currencies')
        return;
      } else if (this.cryptoFirst == '' || this.cryptoSecond == ''){
        alert('Choose 2 currencies')
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
  <h1>Crypto exchanger</h1>
  <Input :setAmount="setAmount" :convert="convert" :toFavorite="toFavorite"/> 
  <div className="selectors">
    <Selector :setCrypto="setCryptoFirst"/>
    <Selector :setCrypto="setCryptoSecond"/>
  </div>
  <h1 v-if="result">{{ amount }} {{ cryptoFirst }} = {{ result }} {{ cryptoSecond }}</h1>
  <Favorites :favorites="favorites" v-if="favorites.length > 0"/>
</template>

<style>

</style>
