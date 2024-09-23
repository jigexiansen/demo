<template>
    <div class="person">
        <h2>姓名：{{ name }}</h2>
        <h2>年龄： {{ age }}</h2>
        <button @click="changeName">修改姓名</button>
        <button @click="changeAge">修改年龄</button>
        <button @click="showTel">显示手机号</button>
    </div>
</template>

<script lang="ts">
export default {
    name: "Person",
    beforeCreate() {
        console.log("beforeCreate")
    },
    setup() {
        // console.log("setup") // setup 函数是先于 beforeCreate 函数初始化的
        // console.log(this) // setup 函数中的 this 是 undefined，vue3 中已经弱化 this 了

        // 定义数据（vue2 数据是定义在 data 函数中的） // vue3 这种数据定义方式不是响应式的，修改数据不会直接反映到页面上
        let name = "cuihua"
        let age = 18
        let tel = "13111111111"

        // 定义方法
        function changeName() {
            name = "haha" // 这样修改 name，页面上是没有变化的
            console.log(name) // name 确实改了，但是不是响应式的
        }

        function changeAge() {
            age++ // 这样修改 age，页面上是没有变化的
            console.log(age) // age 确实改了，但是不是响应式的
        }

        function showTel() {
            alert(tel)
        }

        // 将数据、方法交出去，模板中才可以使用
        // return { name, age, changeName, changeAge, showTel }

        // setup 返回值也可以是一个渲染函数
        return () => "haha"
    }
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