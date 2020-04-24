<template>
  <div class="test">
    <h1>test count: {{ count }}</h1>
    <div>count * 2 {{ doubleCount }}</div>
    <button @click="add">add</button>
    <br />
    <br />
    <br />
    <br />
    <div>当前路由：{{ routeName }}</div>
  </div>
</template>

<script>
 import { ref, computed, watch, getCurrentInstance } from 'vue'

 export default {
   setup () {
     const { ctx } = getCurrentInstance()
     const routeName = ref(ctx.$router.currentRoute.value)
     const count = ref(0)
     const add = () => {
       count.value++
     }
     // 监听
     watch(() => count.value, val => {
       console.log(`count is ${val}`)
     })
     const doubleCount = computed(() => count.value * 2)
     return {
       count,
       add,
       doubleCount,
       routeName
     }
   }
 }
</script>

<style lang="less" scoped>
.test {
  color: red;
}
</style>
