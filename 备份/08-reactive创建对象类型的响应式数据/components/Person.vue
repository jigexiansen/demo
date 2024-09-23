<template>
    <div class="person">
        <h2>汽车信息：一辆{{ car.brand }}车，价值{{ car.price }}万</h2>
        <button @click="changePrice">修改价格</button>
        <hr />
        <h2>游戏列表：
            <ul>
                <li v-for="(game, index) in games" :key="index">
                    {{ game.name }}
                    <button @click="changeName(index)">更改名称</button>
                </li>
            </ul>
        </h2>
        <hr>
        <h2>测试：{{ obj.a.b.c }}</h2>
        <button @click="changObj">更新对象</button>
    </div>
</template>

<script lang="ts" setup name="Person">
import { reactive } from 'vue'; // reactive 只能定义对象类型的响应式数据，ref 既可以定义基本类型又可以定义对象类型的响应式数据
// 数据
let car = reactive({ brand: "奥迪", price: 100 })
// console.log(car)

let games = reactive([
    { id: "1", name: "王者荣耀" },
    { id: "2", name: "原神" },
])
console.log(games)

// 不管对象层级有多深，reactive 函数都能使对象变为响应式
let obj = reactive({
    a: {
        b: {
            c: 666
        }
    }
})

function changePrice(): void {
    car.price += 10
    console.log(car.price)
}

function changeName(index: number): void {
    games[index].name += "啊"
}

function changObj(): void{
    obj.a.b.c = 100
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