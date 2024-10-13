<template>
    <div class="person">
        <!-- v-bind 是单向绑定（数据只能从js到页面，不能从页面到js）, v-bind:value 可以简写为 :value -->
        <!-- v-model 是双向绑定（数据可以从js到页面，也可以从页面到js -->
        姓：<input type="text" v-model="firstName"> <br>
        名：<input type="text" v-model="lastName"> <br>
        姓名：<span>{{ fullName }}</span> <br>
        姓名：<span>{{ fullName }}</span> <br>
        姓名：<span>{{ fullName }}</span> <br>
        <button @click="changeFullName">更改姓名</button>
    </div>
</template>

<script lang="ts" setup name="Person">
import { computed, ref } from 'vue';
let firstName = ref("翠")
let lastName = ref("花")

// computed 和定义函数最大的区别在于，如果返回值值没有改变的情况下，computed会直接返回缓存的值，也就是说返回值没有改变的情况下 console.log(1) 只会打印一次
// computed 返回的 fullName 是只读的，不能改 fullName 变量的值，改了也没效果
// let fullName = computed(() => {
//     console.log(1)
//     return firstName.value + lastName.value
// })

// 但是触发了 fullName 值的更改，可以在 computed 中捕获要更的值，进而在 computed 中进行设置
let fullName = computed({
    get(): string {
        // get 方法的逻辑处理和上面的 computed(() => {}) 效果一样
        console.log(1)
        return firstName.value + lastName.value
    },
    set(v: string) {
        // set 方法能捕获 computedRefImpl 类型的更改值，并加以处理
        console.log(v) // @click="changeFullName" 点击事件触发了值的变更，这里能捕获到更改的值
        const [fn, ln] = v.split('')
        firstName.value = fn
        lastName.value = ln
    }
})
function changeFullName() {
    fullName.value = "哈哈"
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