<template>
  <div id="app">
    <button @click="changeStatus1()">Index</button>
    <button @click="changeStatus2()">Lotto</button>
    <button @click="changeStatus3()">Lunch</button>
    
    <Index v-if="status === 'Index'" />
    <Lotto v-if="status === 'Lotto'" />
    <Lunch v-if="status === 'Lunch'"/>
  </div>
</template>

<script>
import Index from './components/Index.vue'
import Lotto from './components/Lotto.vue'
import Lunch from './components/Lunch.vue'

export default {
  name: 'App',
  components: {
    Index,
    Lotto,
    Lunch
  },
  data: function() {
    return {
      status: 'Index'
    }
  },
  methods: {
    changeStatus1() {
      this.status = 'Index'
      console.log(this.status)
    },
    changeStatus2() {
      this.status = 'Lotto'
      console.log(this.status)
    },
    changeStatus3() {
      this.status = 'Lunch'
      console.log(this.status)
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
