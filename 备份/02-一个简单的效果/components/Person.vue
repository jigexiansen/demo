<template>
    <div class="person">
        <h2>姓名：{{ name }}</h2>
        <h2>年龄：{{ age }}</h2>
        <button @click="changeName">修改姓名</button>
        <button @click="changeAge">修改年龄</button>
        <button @click="showTel">查看手机号</button>
    </div>
</template>

<script lang="ts">
    export default {
        name: "Person", // 组件名称
        data(){
            return {
                name: "cuihua",
                age: 18,
                tel: "13111111111"
            }
        },
        methods: {
            changeName(){
                this.name = "hahaha"
            },
            changeAge(){
                this.age++
            },
            showTel() {
                alert(this.tel)
            }
        }
    }
</script>

<style scoped>
    .person {
       background-color: skyblue; 
       box-shadow: 0 0 10px;
       border-radius: 10px;
       padding: 20px;
    }
    button {
        margin: 0 10px;
    }
</style>