<template>
  <div>
    <h1>Lotto</h1>
    <button @click="getLotto">숫자생성</button>
    <p>{{ lotto }}</p>
  </div>
</template>

<script>
import _ from 'lodash'

export default {
  data() {
    return {
      lotto: ''
    }
  },
  methods: {
    getLotto() {
      this.lotto = _.sortBy(_.sampleSize(_.range(1, 46), 6))
    }
  }
}
</script>

<style>

</style>