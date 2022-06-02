<template v-if="todos">
  <section class="general">
    <div class="general__todos todos">
      <div class="todos__search">
        <p class="todos__search-title">My todos</p>
        <input 
          class="todos__search-inp"
          placeholder="Search"
          v-model="query"
        />
      </div>
      <div class="todos__select">
        <a 
        href=""
        v-on:click="onTodoChange('all')"
        >All</a> /
        <a 
          href=""
          v-on:click="onTodoChange('completed')"
        >Completed</a> / 
        <a 
          href=""
          v-on:click="onTodoChange('noncompleted')"
        >Not Completed</a>
      </div>
      <ul class="todos__list">
        <TodoCard 
          v-bind:todo="todo"
          v-for="todo of selectTodos" :key="todo.id"
        />
      </ul>
    </div>
    <div class="general__bottom"></div>
  </section>
</template>

<script>
import TodoCard from '@/components/TodoCard/TodoCard';

export default {
  props: ['todos'],
  components: {
    TodoCard
  },
  
  data() {
    return {
      query: '',
      value: '',
    }
  },

  methods: {
    onChange () {
      const newQuery = this.query
      this.$emit('add-query', newQuery); 
    },
    onTodoChange(str) {
      event.preventDefault()
      this.value = str;
    }
  },

  computed: {
    searchTodo: function() {
      const allTodos = JSON.parse(JSON.stringify(this.todos))
      if(this.query) {
        return allTodos.filter((tod) => tod.title.includes(this.query.toLowerCase()));
      }

      return allTodos;
    },
    selectTodos: function() {
      if(this.value === 'completed') {
        return this.searchTodo.filter(el => el.completed === true)
      }
      if(this.value === 'noncompleted') {
        return this.searchTodo.filter(el => el.completed === false)
      }
      return this.searchTodo;
    }
  }
}
</script>

<style lang="scss">
  @import './TodoList.scss';
</style>
