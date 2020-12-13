<template>
  <div>
    <div v-for="todo in todos" :key="todo.id">
      <Todoitem v-bind:todo="todo" @del-todo="$emit('del-todo', todo.id)"/>
    </div>
  </div>
</template>

<script>
import Todoitem from './Todoitem'
export default {
   name: "Todos",
   components: {
     Todoitem
   },
   props: ['todos']
};
</script>

<style scoped>
  .list-style {
    display: flex;
    justify-content: start;
  }
</style>