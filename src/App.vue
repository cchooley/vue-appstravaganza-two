<template>
  <div id="app" class="container">
    <h1 class="text-center">Todo App</h1>
    <form @submit.prevent="addTodo()">
      <div class="form-group">
        <label for="newTodo">Add Todo</label>
        <input v-model="newTodo" type="text" class="form-control" id="newTodo" aria-describedby="newTodoHelp" placeholder="Walk the dog?">
        <small id="newTodoHelp" class="form-text text-muted">Enter a new todo.</small>
      </div>
      <button type="submit" class="btn btn-primary">Submit</button>
    </form>
    <ul class="list-group mt-3">
      <li v-for="(todo, i) of todos" class="list-group-item">
        <span :class="{
            isDone: todo.done
          }">{{todo.title}}
        </span>
        <button v-if="!todo.done" @click="markDone(todo)">Done</button>
        <button @click="remove(i)">Delete</button>
      </li>
    </ul>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'app',
  data (){
    return {
      newTodo: '',
      todos: []
    }
  },
  watch: {
    todos: {
      handler() {
        localStorage.todos = JSON.stringify(this.todos)
      },
      deep: true
    }
  },
  mounted() {
    if(localStorage.todos) {
      this.todos = JSON.parse(localStorage.todos)
    }
  },
  methods: {
    addTodo() {
      this.todos.push({
        title: this.newTodo,
        done: false
      });
      this.newTodo = ''
    },
    markDone(todo) {
      todo.done = true;
    },
    remove(index) {
      this.todos.splice(index, 1);
    }
  }
}
</script>

<style>
  @import "https://bootswatch.com/4/litera/bootstrap.min.css";
  .isDone {
    text-decoration: line-through;
  }
</style>
