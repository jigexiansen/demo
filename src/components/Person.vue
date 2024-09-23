<template>
    <div class="person">
        <h2>姓名：{{ p.name }}</h2>
        <h2>年龄：{{ p.age }}</h2>
        <button @click="changeName">更改姓名</button>
        <button @click="changeAge">更改年龄</button>
    </div>
</template>

<script lang="ts" setup name="Person">
import { reactive } from 'vue';

let p = reactive({
    name: "cuihua",
    age: 18,
    address: "前滩中心",
    email: "cuihua@gmail.com",
    tel: "13111111111"
})

function changeName() {
    p.name += "~"
}

function changeAge() {
    p.age++
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