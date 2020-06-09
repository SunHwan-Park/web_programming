# 0609_workshop

### main.js

```js
import Vue from 'vue'
import App from './App.vue'
import router from './router'
import VueCookies from 'vue-cookies' // npm i vue-cookies

Vue.use(VueCookies)

Vue.config.productionTip = false

new Vue({
  router,
  render: h => h(App)
}).$mount('#app')
```

### router/index.js

```js
import Vue from 'vue'
import VueRouter from 'vue-router'
import Home from '../views/Home.vue'

import LoginView from '../views/accounts/LoginView.vue'
import SignupView from '../views/accounts/SignupView.vue'

import CreateView from '../views/articles/CreateView.vue'
import ListView from '../views/articles/ListView.vue'

Vue.use(VueRouter)

  const routes = [
  {
    path: '/',
    name: 'Home',
    component: Home
  },
  {
    path: '/accounts/login',
    name: 'LoginView',
    component: LoginView,
    beforeEnter(from, to, next) {
      if (Vue.$cookies.isKey('auth-token')) {
        next('/')
      } else {
        next()
      }
    }
  },
  {
    path: '/accounts/signup',
    name: 'SignupView',
    component: SignupView,
    beforeEnter(from, to, next) {
      if (Vue.$cookies.isKey('auth-token')) {
        next('/')
      } else {
        next()
      }
    }
  },
  {
    path: '/articles',
    name: 'ListView',
    component: ListView
  },
  {
    path: '/articles/create',
    name: 'CreateView',
    component: CreateView,
    beforeEnter(from, to, next) {
      if (!Vue.$cookies.isKey('auth-token')) {
        next('/accounts/login')
      } else {
        next()
      }
    }
  }
]

const router = new VueRouter({
  mode: 'history',
  base: process.env.BASE_URL,
  routes
})

export default router
```

### App.vue

```vue
<template>
  <div id="app">
    <div id="nav">
      <router-link to="/">Home</router-link> |
      <router-link :to="{ name: 'ListView' }">Articles</router-link> |
      <router-link :to="{ name: 'LoginView' }" v-if="!isLoggedIn">Login</router-link> |
      <router-link :to="{ name: 'SignupView' }" v-if="!isLoggedIn">Sign Up</router-link> |
      <router-link :to="{ name: 'CreateView' }" v-if="isLoggedIn">New Article</router-link> |
      <router-link to="/accounts/logout" v-if="isLoggedIn" @click.native="logout">Logout</router-link>
    </div>
    <router-view @submit-login-data="login" @submit-signup-data="signup" />
    <div v-if="errorMessages">
      <hr>
      {{ errorMessages }}
    </div>
  </div>
</template>

<script>
import axios from 'axios'

const SERVER_URL = 'http://127.0.0.1:8000'

export default {
  name: 'App',
  data() {
    return {
      isLoggedIn: false,
      errorMessages: null,
    }
  },
  methods: {
    setCookie(token) {
      this.$cookies.set('auth-token', token)
      this.isLoggedIn = true
      if (this.errorMessages) {
        this.errorMessages = null
      }
    },

    login(loginData) {
      axios.post(SERVER_URL + '/rest-auth/login/', loginData)
        .then(res => {
          this.setCookie(res.data.key)
          this.$router.push({ name: 'Home' })
        })
        .catch(err => this.errorMessages = err.response.data)
    },

    logout() {
      const config = {
        headers: {
          'Authorization': `Token ${this.$cookies.get('auth-token')}`
        }
      }
      axios.post(SERVER_URL + '/rest-auth/logout/', null, config)
        .then(() => {
          this.$cookies.remove('auth-token')
          this.isLoggedIn = false
          if (this.errorMessages) {
          this.errorMessages = null
          }
          this.$router.push({ name: 'Home' })
        })
        .catch(err => this.errorMessages = err.response.data)
    },

    signup(signupData) {
        axios.post(SERVER_URL + '/rest-auth/signup/', signupData)
        .then(res => {
          this.setCookie(res.data.key)
          this.$router.push({ name: 'Home' })
        })
        .catch(err => this.errorMessages = err.response.data)
    }
  },

  mounted() {
    this.isLoggedIn = this.$cookies.isKey('auth-token')
  },
}
</script>

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

### views/accounts/LoginView.vue

```vue
<template>
  <div>
    <h1>Login</h1>
    <div>
      <label for="username">username: </label>
      <input v-model="loginData.username" id="username" type="text">
    </div>
    <div>
      <label for="password">password: </label>
      <input v-model="loginData.password" id="password" type="password">
    </div>
    <div>
      <button @click="login">Login</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'LoginView',
  data() {
    return {
      loginData: {
        username: null,
        password: null
      }
    }
  },
  methods: {
    login() {
      this.$emit('submit-login-data', this.loginData)
    }
  }
}
</script>

<style>

</style>
```

### views/accounts/SignupView.vue

```vue
<template>
  <div>
    <h1>Sign Up</h1>
    <div>
      <label for="username">username: </label>
      <input v-model="signupData.username" id="username" type="text">
    </div>
    <div>
      <label for="password1">password1: </label>
      <input v-model="signupData.password1" id="password1" type="password">
    </div>
    <div>
      <label for="password2">password2: </label>
      <input v-model="signupData.password2" id="password2" type="password">
    </div>
    <div>
      <button @click="signup">Signup</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'SignupView',
  data() {
    return {
      signupData: {
        username: null,
        password1: null,
        password2: null
      }
    }
  },
  methods: {
    signup() {
      this.$emit('submit-signup-data', this.signupData)
    }
  }
}
</script>

<style>

</style>
```

### views/articles/CreateView.vue

```vue
<template>
  <div>
    <h1>New Article</h1>
    <div>
      <label for="title">Title</label>
      <input v-model="articleData.title" id="title" type="text">
    </div>
    <div>
      <label for="content">Content</label>
      <textarea v-model="articleData.content" id="content" cols="30" rows="10"></textarea>
    </div>
    <div>
      <button @click="createArticle" >Submit</button>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

const SERVER_URL = 'http://127.0.0.1:8000'

export default {
  name: 'CreateView',
  data() {
    return {
      articleData: {
        title: null,
        content: null,
      }
    }
  },
  methods: {
    createArticle() {
      const config = {
        headers: {
          'Authorization': `Token ${this.$cookies.get('auth-token')}`
        }
      }
      axios.post(SERVER_URL + '/articles/create/', this.articleData, config)
        .then(res => {
          this.$router.push({ name: 'ListView' })
          console.log(res)
        })
        .catch(err => console.log(err.response.data))
    }
  }
}
</script>

<style>

</style>
```

### views/articles/ListView.vue

```vue
<template>
  <div>
    <h1>
      Article List
    </h1>
    <ul>
      <li v-for="article in articles" :key="`article_${article.id}`">
        <h5>{{ article.title }}</h5>
        <p>{{ article.content }}</p>
      </li>
    </ul>
  </div>
</template>

<script>
import axios from 'axios'

const SERVER_URL = 'http://127.0.0.1:8000'

export default {
  name: 'ListView',
  data() {
    return {
      articles: []
    }
  },
  methods: {
    fetchArticles() {
      axios.get(SERVER_URL+'/articles/')
        .then(res => this.articles = res.data)
        .catch(err => console.log(err.response.data))
    }
  },
  created() {
    this.fetchArticles()
  }
}
</script>

<style>

</style>
```

