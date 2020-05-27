# 0527_exercise

- `src/App.vue`

  ```vue
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
  ```

- `src/components/Index.vue`

  ```vue
  <template>
    <div>
        <p>사용가능한 기능</p>
        <p>메뉴추천, 로또번호생성</p>
    </div>
  </template>
  
  <script>
  export default {
    name: 'Index'
  }
  </script>
  
  <style>
  
  </style>
  ```

- `src/components/Lotto.vue`

  ```vue
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
  ```

- `src/components/Lunch.vue`

  ```vue
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
  ```

  