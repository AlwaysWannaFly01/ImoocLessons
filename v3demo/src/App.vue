<template>
    <div>
        <p>{{ count }}</p>
        <button @click="handleClick">按钮</button>
        <input type="text" v-model="state2.stu.id">
        <input type="text" v-model="state2.stu.name">
        <input type="text" v-model="state2.stu.age">
        <button @click="addStu">添加</button>
        <ul>
            <li v-for="(stu,index) in state.stus" :key="index" @click="remStu(index)">
                {{ stu.name }} - {{ stu.age }}
            </li>
        </ul>
    </div>
</template>

<script>
import {ref, reactive} from 'vue';

export default {
    name: 'App',
    setup() {
        //定义一个名称叫做count变量,这个变量的初始值是0;
        //这个变量发生改变之后,vue会自动更新ui
        let count = ref(0);

        let {state, remStu} = useRemoveStudent();

        let {state2, addStu} = useAddStudent(state);


        function handleClick() {
            // console.log(count)
            count.value += 1;
        }

        //ref函数只能监听简单类型的变化,不能监听复杂类型的变化

        //注意点:
        //在组合API中定义的变量/方法,想要在外界使用,必须通过return{xxx}暴露出去

        return {count, handleClick, state, remStu, state2, addStu};
    }
}

function useRemoveStudent() {
    let state = reactive({
        stus: [
            {id: 1, name: 'zs', age: 19},
            {id: 2, name: 'ls', age: 12},
            {id: 13, name: 'ww', age: 39},
        ]
    })

    function remStu(index) {
        state.stus = state.stus.filter((stu, idx) => index !== idx)
    }

    return {state, remStu};
}

function useAddStudent(state) {
    let state2 = reactive({
        stu:{
            id: '',
            name: '',
            age: ''
        }
    })

    function addStu(e) {
        e.preventDefault();
        const stu = Object.assign({}, state2.stu);
        console.log(stu)
        state.stus.push(stu)
    }

    return {state2, addStu}
}

</script>
