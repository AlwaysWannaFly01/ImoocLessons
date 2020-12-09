<template>
    <!--    <h1>{{ result }}</h1>-->
    <img :src="result&&result.imgUrl" alt="">
</template>

<script lang="ts">
import {defineComponent} from 'vue'
import axios from 'axios';

export default defineComponent({
    name: "AsyncShow",
    async setup() {
        // return new Promise((resolve, reject) => {
        //     setTimeout(() => {
        //         return resolve({
        //             result: 'Awy'
        //         })
        //     }, 2000)
        // })

        const rawData = await axios.get('https://apiblog.jspang.com/default/getGirl-123')
        return {
            result: rawData.data
        }

    }
})
</script>

<style scoped>

</style>
