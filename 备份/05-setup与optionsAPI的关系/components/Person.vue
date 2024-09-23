<template>
    <div class="person">
        <h2>姓名：{{ name }}</h2>
        <h2>年龄： {{ age }}</h2>
        <button @click="changeName">修改姓名</button>
        <button @click="changeAge">修改年龄</button>
        <button @click="showTel">显示手机号</button>
        <hr />
        <h2>测试1：{{ a }}</h2>
        <h2>测试2：{{ c }}</h2>
        <button @click="b">测试</button>
    </div>
</template>

<script lang="ts">
export default {
    name: "Person",
    beforeCreate() {
        console.log("beforeCreate")
    },
    data() {
        console.log("data")
        // vue2 中的选项式语法可以和 vue3 的组合式语法共存，且 vue2 中可以使用 this 读到 vue3 的 setup 函数中定义的变量，反过来就不能，因为 setup 初始化更早 setup > beforeCreate > data
        return {
            a: 100,
            c: this.name // 可以读到 vue3 中 setup 函数中定义的数据
        }
    },
    methods: {
        b(){
            console.log("b")
        }
    },
    setup() {
        console.log("setup")

        // 定义数据（vue2 数据是定义在 data 函数中的） // vue3 这种数据定义方式不是响应式的，修改数据不会直接反映到页面上
        let name = "cuihua"
        let age = 18
        let tel = "13111111111"
        // let d = a // 读不到 vue2 中 data 定义的数据，更不能使用 this，vue3 弱化了 this（setup 函数中 this 是 undefined）

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
        return { name, age, changeName, changeAge, showTel }
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