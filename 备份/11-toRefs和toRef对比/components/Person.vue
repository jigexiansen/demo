<template>
    <div class="person">
        <h2>姓名：{{ name }}</h2>
        <h2>年龄：{{ age }}</h2>
        <h2>地址：{{ address }}</h2>
        <button @click="changeName">更改姓名</button>
        <button @click="changeAge">更改年龄</button>
        <button @click="changeAddress">更改地址</button>
    </div>
</template>

<script lang="ts" setup name="Person">
import { reactive, toRefs, toRef } from 'vue';

let p = reactive({
    name: "cuihua",
    age: 18,
    address: "前滩中心",
    email: "cuihua@gmail.com",
    tel: "13111111111"
})

// toRefs 可以把对象的所有属性的值包装成响应式数据，且值的更新会直接修改原数据（有点类似于获取到了属性值的地址）
let {name, age} = toRefs(p)

// toRef 只能指定更改对象中的某个确定属性的值为响应式数据
let address = toRef(p, 'address')

// 注意因为使用 toRefs 和 toRef 包装了属性值，所以在改变值时要加 .value 一定不要忘记了
function changeName() {
    name.value += "~"
    console.log(name)
}

function changeAge() {
    age.value++
    console.log(age)
}

function changeAddress() {
    address.value += '.'
    console.log(address)
    
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