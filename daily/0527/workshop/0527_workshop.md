# 0527_workshop

- `src/App.vue`

  ```vue
  <template>
    <div id="app">
      <div id="nav">
        <router-link to="/">Index</router-link> |
        <router-link to="/lunch">Lunch</router-link> |
        <router-link to="/lotto">Lotto</router-link>
      </div>
      <router-view/>
    </div>
  </template>
  
  <style>
  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
  }
  
  #nav {
    padding: 30px;
  }
  
  #nav a {
    font-weight: bold;
    color: #2c3e50;
  }
  
  #nav a.router-link-exact-active {
    color: #42b983;
  }
  </style>
  
  ```

- `src/views/Index.vue`

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

- `src/views/Lotto.vue`

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

- `src/views/Lunch.vue`

  ```vue
  <template>
    <div>
      <h1>Lunch</h1>
      <h3>{{ menus }}</h3>
      <button @click="getMenu">랜덤선택</button>
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

- `src/router/index.js`

  ```js
  import Vue from 'vue'
  import VueRouter from 'vue-router'
  import Index from '../views/Index.vue'
  import Lotto from '../views/Lotto.vue'
  import Lunch from '../views/Lunch.vue'
  
  Vue.use(VueRouter)
  
    const routes = [
    {
      path: '/',
      name: 'Index',
      component: Index
    },
    {
      path: '/lotto',
      name: 'Lotto',
      component: Lotto
    },
    {
      path: '/lunch',
      name: 'Lunch',
      component: Lunch
    }
  ]
  
  const router = new VueRouter({
    mode: 'history',
    base: process.env.BASE_URL,
    routes
  })
  
  export default router
  ```

  