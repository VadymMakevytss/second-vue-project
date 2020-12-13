<template>
  <div>
    <div class="todo-item" v-bind:class="{ 'is-complete': todo.completed }">
      <p>
        <input type="checkbox" v-on:change="markItem" />
        {{ todo.title | uppercase}}
        <button class="del" @click="$emit('del-todo', todo.id)">X</button>
      </p>
    </div>
  </div>
</template>

<script>
export default {
  name: "Todoitem",
  props: ["todo"],
  filters: {
    uppercase(value) {
      return value.toUpperCase()
    }
  },
  methods: {
    markItem() {
      this.todo.completed = !this.todo.completed;
    },
  },
};
</script>

<style scoped>
.todo-item {
  background: #f4f4f4;
  padding: 10px;
  border-bottom: 1px dotted #ccc;
  width: 100%;
  padding: 10px;
  margin-right: 10px;
}

.is-complete {
  text-decoration: line-through;
}

.del {
  background: red;
  color: #fff;
  border: none;
  padding: 5px 9px;
  border-radius: 50%;
  cursor: pointer;
  float: right;
  margin-right: 10px;
}
p {
  text-align: start;
}
</style>