<template>
  <li class="card">
      <p class="card__title">{{ todo.title }}</p>
      <label class="card__switch switch">
        <input 
          type="checkbox"
          class="switch__checkbox checkbox"
          v-model='checked'
        >
        <span class="switch__slider slider"></span>
      </label>
  </li>
</template>

<script>
export default {
    data() {
      return {
        checked: this.todo.completed,
      }
    }, 
    props: {
        todo: {
            type: Object,
            required: true,
        }
    },
}
</script>

<style lang="scss">
  @import './TodoCard.scss';
</style>