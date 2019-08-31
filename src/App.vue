<template>
  <div id="app">
    <Header />
    <AddTodo v-on:add-todo="addTodo"/>
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo" v-on:update-todo="updateTodo"/>
  </div>
</template>

<script>
import Header from './components/layout/Header';
import Todos from './components/Todos';
import AddTodo from './components/AddTodo';
import axios from 'axios';
import moment from 'moment'

export default {
  name: 'app',
  components: {
    Header,
    Todos,
    AddTodo
  },
  data() {
    return {
      serviceUrl: 'http://localhost:3000/todos',
      todos: []
    }
  },
  methods: {
    deleteTodo(id) {
      axios.delete(`${this.serviceUrl}/${id}`)
        .then(this.todos = this.todos.filter((todo) => id !== todo['_id']))
        .catch();
    },
    addTodo(newTodo) {
      const { title, description, date } = newTodo;
      axios.post(this.serviceUrl, {
        title,
        description,
        date
      })
        .then(res => {
          this.todos = [...this.todos, {
            title,
            description,
            date
          }]
        })
        .catch();
    },
    updateTodo(todo) {
      axios.patch(`${this.serviceUrl}/${todo._id}`, {
        title: todo.title,
        description: todo.description,
        date: todo.date
      })
        .then(res => {
          
        })
        .catch();
    }
  },
  created() {
    axios.get(this.serviceUrl)
      .then(res => {
        this.todos = res.data;
        for (let i = 0; i < this.todos.length; i++) {
          this.todos[i].date = moment(String(this.todos[i].date)).format('YYYY-MM-DD');
        }
      })
      .catch();
  }
}
</script>

<style>
  * {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
  }
  body {
    font-family: Arial, Helvetica, sans-serif;
    line-height: 1.4;
  }
  .btn {
    display: inline-block;
    border: none;
    background: #555;
    color: #fff;
    padding: 7px 20px;
    cursor: pointer;
  }
  .btn:hover {
    background: #666;
  }
</style>
