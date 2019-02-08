<template>
  <div id="app">
    <AddTodo v-on:add-todo="addTodo" />
    <list v-bind:impTD="todos" v-on:del-stuff='deleteStuff'/>
  </div>
</template>

<script>
import list from '../components/Todos';
import AddTodo from '../components/AddTodo';
import axios from 'axios';

export default {
  name: 'Home',
  components: {
    list,
    AddTodo
  },
  data() {
      return {
        todos: []
      }
  },
  methods: {
    deleteStuff(id) {
      // Next line is needed only if do not use virtual server
      // Filters out and returns all emelents where id is NOT as selected
      // this.todos = this.todos.filter(todo => todo.id !== id);

        axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
      // Spred operator "..." copies previous content and we add new with "newTdo"
        .then(() => this.todos = this.todos.filter(todo => todo.id !== id))
        .catch(() => console.log('Link is not working')); // eslint-disable-line no-console
    },
    addTodo(newTodo) {
      const { title, completed } = newTodo;
      axios.post('https://jsonplaceholder.typicode.com/todos', {
        title,
        completed
      })
        .then(res => this.todos = [...this.todos, res.data])
        .catch(()=> console.log('Link is not working')); // eslint-disable-line no-console
    }
  },
  created () {
    // "limit=5" means how much to get from virtual server
    axios.get('https://jsonplaceholder.typicode.com/todos?_limit=10')
    .then(res => this.todos = res.data)
    .catch(err => console.log(err)); // eslint-disable-line no-console
  }
}
</script>
