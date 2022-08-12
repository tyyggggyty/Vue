<template>
  <div>
    <MyHeader @addTodo="addTodo" />
    <MyList :todos="todos" />
    <MyFooter
      :todos="todos"
      @checkAllTodo="checkAllTodo"
      :deleteDoneTodo="deleteDoneTodo"
    />
  </div>
</template>

<script>
import MyHeader from "./components/MyHeader";
import MyList from "./components/MyList";
import MyFooter from "./components/MyFooter";
export default {
  name: "App",
  components: { MyHeader, MyList, MyFooter },
  data() {
    return {
      todos: JSON.parse(localStorage.getItem("todos")) || [],
    };
  },
  methods: {
    addTodo(todo) {
      this.todos.unshift(todo);
    },

    checkTodo(id) {
      this.todos.forEach((todo) => {
        if (todo.id === id) todo.done = !todo.done;
      });
    },

    deleteTodo(id) {
      this.todos = this.todos.filter((todo) => todo.id != id);
    },

    checkAllTodo(done) {
      this.todos.forEach((todo) => {
        todo.done = done;
      });
    },

    deleteDoneTodo() {
      this.todos = this.todos.filter((todo) => !todo.done);
    },
    editTodo(todo) {
      todo.isEdit = true;
    },
    updateTodo(todo, title) {
      todo.isEdit = false;
      if (title.trim()) todo.title = title;
    },
  },
  watch: {
    todos: {
      deep: true,
      handler(value) {
        localStorage.setItem("todos", JSON.stringify(value));
      },
    },
  },
  mounted() {
    this.$bus.$on("checkTodo", this.checkTodo);
    this.$bus.$on("deleteTodo", this.deleteTodo);
    this.$bus.$on("editTodo", this.editTodo);
    this.$bus.$on("updateTodo", this.updateTodo);
  },
  beforeDestroy() {
    this.$bus.$off("checkTodo");
    this.$bus.$off("deleteTodo");
    this.$bus.$off("editTodo");
    this.$bus.$off("updateTodo");
  },
};
</script> 

<style>
/*base*/
body {
  width: 600px;
  background: #fff;
  border: 1px solid rgb(176, 176, 176);
  box-sizing: border-box;
  padding: 10px;
  margin: 200px auto;
}
.btn {
  display: inline-block;
  padding: 4px 12px;
  margin-bottom: 0;
  font-size: 14px;
  line-height: 20px;
  text-align: center;
  vertical-align: middle;
  cursor: pointer;
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.2),
    0 1px 2px rgba(0, 0, 0, 0.05);
  border-radius: 4px;
}
.btn-danger {
  color: #fff;
  background-color: #da4f49;
  border: 1px solid #bd362f;
}
.btn-edit {
  color: #fff;
  background-color: #3157eb;
  border: 1px solid #2344c6;
}
.btn-danger:hover {
  color: #fff;
  background-color: #bd362f;
}
.btn-edit:hover {
  color: #fff;
  background-color: #2344c6;
}
.btn:focus {
  outline: none;
}
.todo-container {
  width: 600px;
  margin: 0 auto;
}
.todo-container .todo-wrap {
  padding: 10px;
  border: 1px solid #ddd;
  border-radius: 5px;
}
</style>
