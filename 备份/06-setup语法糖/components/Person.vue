<template>
    <div class="person">
        <h2>姓名：{{ name }}</h2>
        <h2>年龄： {{ age }}</h2>
        <h2>地址： {{ address }}</h2>
        <button @click="changeName">修改姓名</button>
        <button @click="changeAge">修改年龄</button>
        <button @click="showTel">显示手机号</button>
    </div>
</template>

<!-- <script lang="ts"> 
/* 
不能和 setup 语法糖写在一起，打消这个念头！，既然不能合一起，那就干脆不写了，直接删掉，但是删除后有个问题：组件的名称不好控制了，组件名默认是文件名，但是可以借助一个插件来实现这个功能：npm i vite-plugin-vue-setup-extend -D ，安装完成后，在项目根目录的 vite.config.ts 中使用 import 导入该组件： import VueSetupExtend from "vite-plugin-vue-setup-extend" ，导入后在导入的地方下面 plugins 中调用该组件即可：
plugins: [
    vue(),
    VueSetupExtend(),
]
*/

export default {
    name: "Person",
}
</script> -->

<script lang="ts" setup name="Person11"> // 设置好 vite-plugin-vue-setup-extend 组件后，就可以在 script 标签增加 name 属性来定义组件名称啦啦~
// setup 语法糖，只需关注定义，不用显式的交出去

// 定义数据
let name = "cuihua"
let age = 18
let tel = "13111111111"
let address = "上海市浦东新区前滩中心"

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