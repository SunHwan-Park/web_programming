<template>
  <div>
    <h1>Lunch</h1>
    <button @click="getMenu">랜덤선택</button>
    <h3>{{ menus }}</h3>
    <p>{{ sltMenu }}</p>
  </div>
</template>

<script>
import _ from 'lodash'

export default {
    name: 'Lunch',
    data: function() {
        return {
            menus: ['짜장', '짬뽕', '김밥', '라면'],
            sltMenu: ''
        }
    },
    methods: {
        getMenu() {
            this.sltMenu = _.sampleSize(this.menus, 1)[0]
        }
    }
}
</script>

<style>

</style>