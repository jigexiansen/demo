<template>
    <div class="person">
        <h1>情况四：监视 ref 或 reactive 定义的响应式对象中的属性</h1>
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

// 监视，情况四：监视 ref 或 reactive 定义的响应式对象中的属性，且该属性的值是基本类型，要写成 getter 函数 (getter 函数就是 一个函数返回一个值)
// watch(() => person.name, (newValue, oldValue) => {
//     console.log(newValue, oldValue)
// })

// 监视，情况四：监视 ref 或 reactive 定义的响应式对象中的属性，且该属性的值是对象类型，可以直接写该属性，也可以写成 getter 函数，
// 1. 直接写该属性时，如果属性的值（注意该值是一个对象）的属性有改变，这种是能监视到的，但是如果该对象直接被覆盖了（地址变了）是不能被监视到的，比如 person.car = { c1: "奔驰3", c2: "宝马3" } 直接覆盖了 person.car 就监视不到了
// watch(person.car, (newValue, oldValue) => {
//     console.log(newValue, oldValue)
// })

// 2. 写 getter 函数时，如果属性的值（注意该值是一个对象）的属性有改变，这种是监视不到的，但是如果该对象直接被覆盖了（地址变了）可以被监视到，比如 person.car = { c1: "奔驰3", c2: "宝马3" } 直接覆盖了 person.car 这种修改是能被监视到的
// 如果想监视 person.car 对象的变化同时也见识 该对象的属性值是否有变化，开启深度监视即可 
// ！！此种方法是推荐用法，可以和监视对象基本类型属性值保持一直的写法（就是都写成 getter 函数），然后如果想监视对象属性的属性值，开启一下深度监视就可以了
watch(()=> person.car, (newValue, oldValue) => {
    console.log("person.car 变化了", newValue, oldValue)
},
{ deep: true } // 如果需要监视对象属性的值的属性是否有变化，开启深度监视就好了
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