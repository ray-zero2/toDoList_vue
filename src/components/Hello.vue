<template>
  <div>
    {{ msg }}
    <form>
      <button @click.prevent="addTodo()">ADD TASK</button>
      <button @click.prevent="removeTodo()">DELETE FINISHED TASKS</button>
      <p>
        input:
        <input type="text" v-model="newTodo">
      </p>
      <p>task:</p>
      <p v-if="newTodo.length > 0">{{newTodo}}</p>
      <p v-else>no-input</p>
    </form>
    <div class="task-list">
      <label class="task-list__item" v-for="(todo,index) in todos" :key="index">
        <input type="checkbox" v-model="todo.done">
        <!-- <button>EDIT</button> -->
        {{ todo.text }}
      </label>
    </div>
  </div>
</template>

<script>
export default {
  name: "Hello",
  data() {
    return {
      msg: "Welcome to Your Vue.js App",
      todos: [
        { text: "vue-router", done: false },
        { text: "vuex", done: false },
        { text: "vue-loader", done: false },
        { text: "awesome-vue", done: true },
        { text: "vue-is-so-difficult", done: true }
      ],
      newTodo: ""
    };
  },
  methods: {
    addTodo() {
      let text = this.newTodo && this.newTodo.trim();
      if (!text) {
        return;
      }
      this.todos.push({
        text: text,
        done: false
      });
      this.newTodo = "";
    },
    removeTodo() {
      for (let i = this.todos.length - 1; i >= 0; i--) {
        if (this.todos[i].done) this.todos.splice(i, 1);
      }
    }
  }
};
</script>
