<template>
  <div class="test">
    <h1>test count: {{ count }}</h1>  <br />
    <div>count * 2 {{ doubleCount }}</div>  <br />
    <div>state from vuex {{a}}</div>  <br />
    <div>当前路由：{{ routeName.fullPath }}</div>  <br />
    <br />
    <button @click="add">add</button>
    <button @click="update">update a</button>
  </div>
</template>

<script>
 import { ref, computed, watch, getCurrentInstance } from 'vue'

 export default {
   setup () {
     const { ctx } = getCurrentInstance()
     const count = ref(0)
     const add = () => {
       count.value++
     }
     // 监听
     watch(() => count.value, val => {
       console.log(`count is ${val}`)
     })
     const doubleCount = computed(() => count.value * 2)
     // 获取当前route info
     const routeName = ref(ctx.$router.currentRoute.value)
     const a = computed(() => ctx.$store.state.test.a)
     const update = () => {
       ctx.$store.commit('setTestA', count)
     }
     return {
       count,
       add,
       doubleCount,
       routeName,
       a,
       update
     }
   }
 }
</script>

<style lang="less" scoped>
.test {
  color: red;
}
</style>
