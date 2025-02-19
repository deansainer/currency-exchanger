<script>
export default{
    props: {
        setAmount: {
            type: Function,
            required: true
        },

        convert: {
            type: Function,
            required: true
        },
        
    }
}
</script>

<template>
  <input min="0" type="number" @input="setAmount($event.target.value)"><br>
  <button @click="convert()">Convert</button>
</template>

<style scoped>

input{
    text-align: center;
    width: 238px;
    border-radius: 4px;
    background-color: white;
    border: 1 px solid white;
    outline: none;
    padding: 6px;
}

button{
    width: 120px;
    height: 35px;
    background-color: rgb(24, 70, 88);
    color: white;
    border: 0px;
    border-radius: 10px;
    margin-top: 20px;
    cursor: pointer;
}
</style>
