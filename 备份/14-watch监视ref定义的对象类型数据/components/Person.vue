<template>
    <div class="person">
        <h1>情况二：监视【ref】定义的【对象类型】数据</h1>
        <h2>姓名：{{ person.name }}</h2>
        <h2>年龄：{{ person.age }}</h2>
        <button @click="changeName">更改姓名</button>
        <button @click="changeAge">更改年龄</button>
        <button @click="changePerson">更改整个人</button>
    </div>
</template>

<script lang="ts" setup name="Person">
import { ref, watch } from 'vue'

// 数据
let person = ref({
    name: 'cuihua',
    age: 18
})

// 方法
function changeName() {
    person.value.name += '~'
}

function changeAge() {
    person.value.age += 1
}

function changePerson() {
    person.value = { name: "haha", age: 20 }
}

// 监视，情况二：监视【ref】定义的【对象类型】数据，监视的是对象的地址值，要是想监视对象内部属性的变化，需要手动开启深度监视
// 如果监视的是对象：
//    修改的是 ref 定义的对象中的属性， newValue 和 oldValue 都是新值，因为他们是同一个对象
//    修改整个 ref 定义的对象，newValue 是新值，oldValue 是旧值，因为不是同一个对象了
// watch 的第一个参数是：被监视的数据
// watch 的第二个参数是：监视的回调
// watch 的第三个参数是：配置对象（deep、immediate等）
const stopWatch = watch(person, (newValue, oldValue) => {
    console.log("person 变化了", newValue, oldValue)
}, { deep: true, immediate: true }) // deep 是监视对象的属性只要有变化，就会有 newValue 产生，immediate 为 true时是先开启监视，false 时是第一次触发监视时开始监视
</script>

<style scoped>
.person {
    box-shadow: 0 0 0 0;
    background-color: skyblue;
    border-radius: 10px;
    padding: 20px;
}

button {
    margin: 0 10px;
}
</style>