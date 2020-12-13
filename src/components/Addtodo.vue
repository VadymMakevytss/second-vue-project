<template>
  <div>
    <form @submit="addTodo">
      <input
        v-model="title"
        type="text"
        name="title"
        placeholder="Add Todo ..."
      />
      <input type="submit" value="Submit" class="btn" />
    </form>
  </div>
</template>
 
 <script>
//import { v4 as uuidv4 } from "uuid";
export default {
  name: "AddTodo",
  data() {
    return {
      title: "",
    };
  },
  methods: {
    addTodo(event) {
      event.preventDefault();
      const newTodo = {
        //id: uuidv4(),
        title: this.title,
        completed: false,
      };
      // Send to parent
      this.$emit("add-todo", newTodo);
      this.title = "";
    },
  },
};
</script>

 <style scoped>
form {
  margin-top: 10px;
  display: flex;
}
input[type="text"] {
  flex: 10;
  padding: 5px;
}
input[type="submit"] {
  flex: 2;
}
</style>