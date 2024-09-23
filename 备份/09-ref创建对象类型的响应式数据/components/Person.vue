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
    </div>
</template>

<script lang="ts" setup name="Person">
import { reactive, ref } from 'vue';
// 使用 ref 定义对象类型的响应式数据
let car = ref({ brand: "奥迪", price: 100 })

// 使用 reactive 定义对象类型的响应式数据
let obj = reactive({x:666})
// 对比数据可以发现：ref 定义对象类型的响应式数据，实际上底层还是使用的 reactive 实现的，所以 ref 定义的对象类型响应式数据也是深层级的
console.log(car)
console.log(obj)

let games = ref([
    { id: "1", name: "王者荣耀" },
    { id: "2", name: "原神" },
])
// console.log(games)


function changePrice(): void {
    car.value.price += 10
    console.log(car.value.price)
}

function changeName(index: number): void {
    games.value[index].name += "啊"
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