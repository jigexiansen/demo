<template>
    <div class="person">
        <h1>情况五：监视上述多个数据</h1>
        <h2>姓名：{{ person.name }}</h2>
        <h2>年龄：{{ person.age }}</h2>
        <h2>第一台车：{{ person.car.c1 }}、第二台车：{{ person.car.c2 }}</h2>
        <button @click="changeName">修改姓名</button>
        <button @click="changeAge">修改年龄</button>
        <button @click="changeC1">修改第一台车</button>
        <button @click="changeC2">修改第二台车</button>
        <button @click="changeCar">修改整个车</button>
    </div>
</template>

<script lang="ts" setup name="Person">
import { reactive, watch } from 'vue';

let person = reactive({
    name: '张三',
    age: 18,
    car: {
        c1: "奔驰",
        c2: "宝马"
    }
})

function changeName(): void {
    person.name += "~"
}

function changeAge(): void {
    person.age++
}

function changeC1(): void {
    person.car.c1 = "奔驰2"
}

function changeC2(): void {
    person.car.c2 = "宝马2"
}

// 注意 reactive 定义的响应式对象，对象值是不能直接更改的，要使用 Object.assign() 覆盖所有属性的值，
// 但是 reactive 定义的响应式对象的属性的值如果是一对象，可以直接覆盖这个属性的值
function changeCar(): void {
    person.car = { c1: "奔驰3", c2: "宝马3" } // 这种写法改变了对象属性的值的地址，所以必须在坚实的时候使用 getter 函数，且监视新对象属性值变化时，开启深度监视即可
    // Object.assign(person.car, { c1: "奔驰3", c2: "宝马3" }) // 如果写成这种覆盖属性值的形式，就可以在监视属性值为对象类型的时候写成属性的形式
}

// 监视，情况五：监视上述多个数据
// 使用数组把监视对象放入数组中，可以监视多个对象属性，如果需要监视对象属性值的变化，需要开启深度监视
watch([() => person.name, () => person.age, () => person.car], (newValue, oldValue) => {
    console.log("person.car 变化了", newValue, oldValue)
}, { deep: true })

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