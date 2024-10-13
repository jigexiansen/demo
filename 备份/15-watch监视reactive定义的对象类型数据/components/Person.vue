<template>
    <div class="person">
        <h1>情况三：监视【reactive】定义的【对象类型】数据</h1>
        <h2>姓名：{{ person.name }}</h2>
        <h2>年龄：{{ person.age }}</h2>
        <button @click="changeName">更改姓名</button>
        <button @click="changeAge">更改年龄</button>
        <button @click="changePerson">更改整个人</button>
    </div>
</template>

<script lang="ts" setup name="Person">
import { reactive, watch } from 'vue'

// 数据
let person = reactive({
    name: 'cuihua',
    age: 18
})

// 方法
function changeName() {
    person.name += '~'
}

function changeAge() {
    person.age += 1
}

function changePerson() {
    Object.assign(person, { name: "haha", age: 20 })
}

// 监视，情况三：监视【reactive】定义的【对象类型】数据，默认是开启了深度监视的
//（注意，这个监视是不可以关闭的，就算第三个参数设置了 {deep:false}，也没有任何效果）
watch(person, (newValue, oldValue) => {
    console.log('person', newValue, oldValue)
}
// , { deep: false } // 使用 reactive 定义的响应式对象，默认开启深度监视，且是不可关闭的
)

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