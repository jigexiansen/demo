<template>
    <div class="person">
        <h1>情况一：监视【ref】定义的【基本类型】数据</h1>
        <h2>当前求和为：{{ sum }}</h2>
        <button @click="changeSum">点我sum+1</button>
    </div>
</template>

<script lang="ts" setup name="Person">
import { ref, watch } from 'vue'

// 数据
let sum = ref(0)

// 方法
function changeSum() {
    sum.value += 1
}

// 监视，情况一：监视【ref】定义的【基本类型】数据
const stopWatch = watch(sum, (newValue, oldValue) => {
    console.log('sum变化了', newValue, oldValue)
    if (sum.value >= 10) {
        stopWatch() // 停止当前监视
    }
})

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