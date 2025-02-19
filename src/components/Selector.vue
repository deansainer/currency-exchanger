<script>
export default{
    props: {
        setCrypto: {
            type: Function,
            required: true
        }
    },
    data(){
        return{
            current: ''
        }
    },
    methods: {
        selectItem(val){
            this.setCrypto(val)
            this.current = val
        }
    }
}
</script>

<template>
    <ul>
        <li @click="selectItem('BTC')" :className="current == 'BTC' ? 'active': ''">Bitcoin</li>
        <li @click="selectItem('ETH')" :className="current == 'ETH' ? 'active': ''">Etherium</li>
        <li @click="selectItem('USDT')" :className="current == 'USDT' ? 'active': ''">USDT</li>
    </ul>
</template>

<style scoped>

ul {
    list-style: none;
    width: 238px;
    padding: 0px;
    border-radius: 3px;
    border: 1px solid rgb(53, 53, 53);
}

li{
    display: block;
    background-color: rgb(47, 109, 126);
    color: white;
    padding: 20px 0;
    border: 1px solid rgb(53, 53, 53);
}

li:hover, li.active{
    background-color: rgb(74, 153, 175);
    cursor: pointer;
}

</style>
