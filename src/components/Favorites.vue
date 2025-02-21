<template>
    <div v-for="(pair, index) in favorites" :key="index">
        <span>{{ pair }}</span>
    </div>
</template>

<script>
export default {
    props: {
        favorites: {
        type: Array,
        required: true
        }
    }
}
</script>

<style>

</style>