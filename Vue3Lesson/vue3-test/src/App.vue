<template>
    <img alt="Vue logo" src="./assets/logo.png">
    <div>
        <button v-for="(item,index) in people" :key="index" @click="selectFun(index)">
            {{ item }}:{{ index }}
        </button>
        <p>选择了[{{ selectedPeron }}]</p>
    </div>
    <div v-if="loading">loading...</div>
    <!--    <img :src="result.imgUrl" v-if="loaded">-->
    <Modal></Modal>
    <Suspense>
        <template #default>
            <AsyncShow/>
        </template>
        <template #fallback>
            <h1>loading...</h1>
        </template>
    </Suspense>
</template>

<script lang="ts">
import {
    reactive,
    toRefs,
    onBeforeMount,
    onMounted,
    onBeforeUpdate,
    onUpdated,
    onRenderTracked,
    onRenderTriggered,
    watch,
    onErrorCaptured
} from 'vue';
import userUrlAxios from "@/hooks/useURLAxios";
import Modal from '@/components/Modal.vue';
import AsyncShow from "@/components/AsyncShow.vue";

interface DataProps {
    people: string[];
    selectedPeron: string;
    selectFun: (index: number) => void;
}

export default {
    name: 'App',
    components: {
        Modal,
        AsyncShow
    },
    setup() {
        console.log('1-开始创建组件---setup()');
        const data: DataProps = reactive({
            people: ['张三', '李四', '王五'],
            selectedPeron: "",
            selectFun: (index: number) => {
                data.selectedPeron = data.people[index]
            }
        })

        onBeforeMount(() => {
            console.log('2-组件挂载到页面之前执行---onBeforeMount()');
        })

        onMounted(() => {
            console.log('3-组件挂载到页面之后执行---onMounted()');
        })

        onBeforeUpdate(() => {
            console.log('4-组件更新之前执行---onBeforeUpdate()');
        })

        onUpdated(() => {
            console.log('5-组件更新之后执行---onUpdated()');
        })

        // onRenderTracked((event) => {
        //     console.log('状态跟踪钩子函数');
        //     console.log(event)
        // })

        onRenderTriggered((event) => {
            console.log('状态跟踪钩子函数');
            console.log(event)
        })

        onErrorCaptured((error) => {
            //捕获接口出错的异常
            console.log('error ==>', error)
            return true
        })
        //onBeforeUnmount()组件卸载之前执行
        //onUnmounted()组件卸载

        //onActivated()  <keep-alive></keep-alive>
        //onDeactivated()

        //onErrorCaptured()  子组件异常时激活该函数

        const refData = toRefs(data);

        const {result, loading, loaded} = userUrlAxios('https://apiblog.jspang.com/default/getGirl');

        return {
            ...refData,
            result,
            loading,
            loaded
        }
    }
};

</script>

<style>
#app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
}
</style>

