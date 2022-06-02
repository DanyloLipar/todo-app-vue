<template>
  <div class="add">
    <p class="add__title">Add Todo</p>
    <form 
      class="add__items"
      @submit.prevent="onSubmit"
    >
        <input 
            class="add__items-input"
            placeholder="Todo name"
            v-model="title"
        />
        <button
          type="submit" 
          class="add__items-btn btn"   
          >
            <p class="btn__text">+</p>
        </button>
    </form>
  </div>
</template>

<script>
export default {
  methods: {
    props: ['todos'],
    
    data() {
      return {
        title: '',
      }
    },

    onSubmit () {
      if(this.title.trim()) {
        const newTodo = {
          userId: Date.now(),
          id: 1,
          title: this.title,
          completed: false,
        }

        this.$emit('add-todo', newTodo)
        this.title = '';
      }
    }
  }
}
</script>

<style lang="scss">
@import './AddTodo.scss';


</style>