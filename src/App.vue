<template>
  <div id="app">
    <Header />
    <AddTodo v-on:add-todo="addTodo" />
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo" />
  </div>
</template>

<script>
import Todos from './components/Todos';
import Header from './components/layout/Header';
import AddTodo from './components/AddTodo';

export default {
  name: 'app',
  components: {
    Header,
    Todos,
    AddTodo
  },
  data() {
    return {
      todos: []
    }
  },
  watch : {
    // todos:function() {
    //   localStorage.setItem('todos',JSON.stringify(this.todos));
    //   alert('Data saved!');
    // }
    todos: {
      handler:function() {
        localStorage.setItem('todos',JSON.stringify(this.todos));
        // alert('Data saved!');
      },
      deep:true
    }
  },
  mounted:function() {
    this.todos = JSON.parse(localStorage.getItem('todos')) ||[];
  },
  methods :{
    deleteTodo(id) {
      this.todos = this.todos.filter(todo => todo.id !== id)
    },
    addTodo(newTodo) {
      this.todos = [...this.todos,newTodo]
    }
  },
}
</script>

<style>
  * {
    box-sizing: border-box;
    margin:0;
    padding: 0;
  }
  body {
    font-family: Arial, Helvetica, sans-serif;
    line-height: 1.4;
  }

  .btn {
    display: inline-block;
    border: none;
    background-color: #555;
    color: #fff;
    padding: 7px 20px;
    cursor: pointer;
  }

  .btn:hover {
    background-color: #666;
  }
</style>
