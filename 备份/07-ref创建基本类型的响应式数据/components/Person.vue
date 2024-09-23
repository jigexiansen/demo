<template>
    <div class="person">
        <h2>姓名：{{ name }}</h2> <!-- 模板中 name.value 会自动解析为 name -->
        <h2>年龄： {{ age }}</h2> <!-- 模板中 age.value 会自动解析为 age -->
        <h2>地址： {{ address }}</h2>
        <button @click="changeName">修改姓名</button>
        <button @click="changeAge">修改年龄</button>
        <button @click="showTel">显示手机号</button>
    </div>
</template>

<script lang="ts" setup name="Person">
import { ref } from "vue"; // 引入定义‘基本类型’响应式数据函数 ref，vue3 的 ref 函数和 vue2 的 ref 不是同一个东西，别搞混了

// 定义数据
let name = ref("cuihua") // 定义响应式数据（使用 ref 函数把响应式数据包起来）
let age = ref(18) // 定义响应式数据（使用 ref 函数把响应式数据包起来）
let tel = "13111111111" // 给有变化的数据定义响应式，没变化就没必要定义响应式数据
let address = "上海市浦东新区前滩中心"

console.log(1, name)
console.log(2, age)
console.log(3, tel)
console.log(4, address)

// 定义方法
function changeName() {
    name.value = "haha" // ts 代码里必须要使用 name.value 的写法，而不能偷懒写成模版中的 name 简写，不然不是响应式数据
    console.log(name.value)
}

function changeAge() {
    age.value++
    console.log(age.value)
}

function showTel() {
    alert(tel)
}
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