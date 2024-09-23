<template>
    <div class="person">
        <h2>汽车信息：一辆{{ car.brand }}车，价值{{ car.price }}万</h2>
        <button @click="changeBrand">修改品牌</button>
        <button @click="changePrice">修改价格</button>
        <button @click="changeCar">修改汽车</button>
        <hr />
        <h2>当前求和为：{{ sum }}</h2>
        <button @click="changeSum">点我sum+1</button>
    </div>
</template>

<script lang="ts" setup name="Person">
import { reactive, ref } from 'vue';

// 使用 reactive 定义对象类型响应数据，不能够二次赋值整个对象，因为覆盖后就不是响应式了，可以理解为指针的地址变了
// 但是使用 ref 定义对象类型响应数据，就不会有这个问题，只需要记住 ref.value 永远是响应式的，可以理解为 ref.value 改变的是指针地址的值
let car = reactive({ brand: "奥迪", price: 100 }) 
let sum = ref(0) 

function changeBrand(): void {
    car.brand = "宝马"
}

function changePrice(): void {
    car.price += 10
}

function changeCar(): void {
    // car = { brand: "奥拓", price: 1 } // reactive 定义的对象类型这么写页面是不会更新的，但是 ref 定义的对象类型就没问题（注意使用 ref 定义时更改的是 car.value 而不是 car）
    // car = reactive({ brand: "奥拓", price: 1 }) // reactive 定义的对象类型这么写页面是不会更新的

    // reactive 定义的对象类型可以这么写，来保持响应式，虽然是响应式的，但是但是如果有 100 个字段，要写 100 次？
    // car.brand = "奥拓"
    // car.price = 1

    // reactive 定义的对象类型使用原生对象的 assign 方法来处理不是响应式的情况：使用 Object.assign(obj1, obj2, obj3) 覆盖定义的对象类型的属性值 // 把 obj2、obj3 的属性给 obj1
    Object.assign(car, { brand: "奥拓", price: 1 })
    console.log(car)
}

function changeSum(): void {
    sum.value += 1
}

/*
Tips: ref 和 reactive 使用原则：
如果定义基本类型的响应式数据，只能 ref
如果定义对象类型的响应式数据，且对象层级不深，ref、reactive 都行
如果定义对象类型的响应式数据，切对象层级很深，建议 reactive，不然大量的 refData.value 看着就很难受
*/
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