<template>
  <div class="box">
    <div class="box__heading"></div>
    <section class="box__content content">
      <h1 class="content__desc">Todo App</h1>
      <div class="content__blocks">
        <AddTodo 
          @add-todo="todoAdder"
        />
        <TodoList 
          v-bind:todos="todos"
        />
      </div>
    </section>
  </div>
</template>

<script>
  import TodoList from '@/components/TodoList/TodoList';
  import AddTodo from '@/components/AddTodo/AddTodo';
export default {
  name: 'app',
  
  data() {
    return {
      todos: [],
    }
  },

  mounted() {
    this.todos = JSON.parse(localStorage.getItem('todos'))
    if(!JSON.parse(localStorage.getItem('todos'))) {
    fetch('https://jsonplaceholder.typicode.com/todos')
      .then(response => response.json())
      .then(resp => {
        this.todos = resp
      })
    }
  },

  components: {
    TodoList,
    AddTodo,
  },

  methods: {
    todoAdder(todo) {
      this.todos.unshift(todo);
    },
  },
}
</script>

<style lang="scss">
 @import './styles/App.scss';
</style>
