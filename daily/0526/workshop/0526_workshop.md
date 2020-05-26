# 0526_workshop

- `todo_list_vue.html`

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>0526 workshop</title>
    <style>
      /* 취소선 */
      .isCompleted {
        text-decoration: line-through;
      }
    </style>
  </head>
  <body>
    <!-- 여기에 코드를 작성하시오 -->
    <div id="app">
      <h1>Todo 앱</h1>
      <select v-model="status">
        <option value="all">전체</option>
        <option value="active">진행중</option>
        <option value="completed">완료</option>
      </select>
      <ul>
        <li v-for="todo in todoByStatus" v-bind:class="{isCompleted: todo.completed}" v-bind:key="todo.id">
          <input type="checkbox" v-model="todo.completed">
          <span>{{ todo.content }}</span>
        </li>
      </ul>
      <div>
        <input v-on:keyup.enter="addTodo" v-model="newInput" type="text">
        <button @click="addTodo">+</button>
      </div>
      <button @click="clearCompleted">완료된 할 일 지우기</button>
    </div>
  
    <script src="https://unpkg.com/axios/dist/axios.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <script>
      // 여기에 코드를 작성하시오
      const app = new Vue({
        el: '#app',
        data: {
          status:
          newInput: '',
          todos: [
            {
              id: 1,
              content: 'Django 복습',
              completed: true
            },
            {
              id: 2,
              content: 'JavaScript 복습',
              completed: false
            },
            {
              id: 3,
              content: 'Vue JS 복습',
              completed: false
            }
          ]
        },
        methods: {
          check(todo) {
            todo.completed = !todo.completed
          },
          addTodo() {
            this.todos.push({
              id: Date.now(),
              content: this.newInput,
              completed: false
            })
            this.newInput = ''
          },
          clearCompleted() {
            this.todos = this.todos.filter(todo => !todo.completed)
          }
        },
        computed: {
          todoByStatus() {
            if (this.status === 'active') {
              return this.todos.filter(todo => !todo.completed)
            }
            if (this.status === 'completed') {
              return this.todos.filter(todo => todo.completed)
            }
            return this.todos
          }
        }
      })
    </script>
  </body>
  </html>
  ```