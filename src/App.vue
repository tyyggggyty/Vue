<template>
  <div>
    <MyHeader :addTodo="addTodo" />
    <MyList :todos="todos" :checkTodo="checkTodo" :deleteTodo="deleteTodo" />
    <MyFooter :todos="todos" :checkAllTodo="checkAllTodo" :deleteDoneTodo="deleteDoneTodo" />
  </div>
</template>

<script>
import MyHeader from "./components/MyHeader";
import MyList from "./components/MyList";
import MyFooter from "./components/MyFooter";
export default {
  name: "app",
  components: { MyHeader, MyList, MyFooter },
  data() {
    return {
      todos: [
        { id: "001", title: "打游戏", done: true },
        { id: "002", title: "学习", done: false },
        { id: "003", title: "睡觉", done: true },
      ],
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
        todo.done = done
      });
    },

    deleteDoneTodo() {
      this.todos = this.todos.filter((todo) => !todo.done );
    }
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
.btn-danger:hover {
  color: #fff;
  background-color: #bd362f;
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
