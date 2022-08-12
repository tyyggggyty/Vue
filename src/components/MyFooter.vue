<template>
  <div class="todo-footer" v-show="total">
    <label>
      <!-- <input type="checkbox" :checked="allDone"  @change="changeAll"/> -->
      <input type="checkbox" v-model="allDone" />
    </label>
    <span>
      <span>已完成{{ doneTotal }}</span> / 全部{{ total }}
    </span>
    <button class="btn btn-danger" @click="deleteDoneTodo">
      清除已完成任务
    </button>
  </div>
</template>

<script>
export default {
  name: "MyFooter",
  data() {
    return {
      sum: 0,
    };
  },
  //   props: ["todos", "checkAllTodo","deleteDoneTodo"],
  props: ["todos", "deleteDoneTodo"],
  computed: {
    total() {
      return this.todos.length;
    },

    doneTotal() {
      return this.todos.reduce((pre, todo) => pre + (todo.done ? 1 : 0), 0);
    },

    allDone: {
      get() {
        return this.doneTotal == this.total && this.total > 0;
      },
      set(value) {
        this.$emit("checkAllTodo", value);
      },
    },
  },
  //   methods: {
  //     changeAll(e) {
  //       this.checkAllTodo(e.target.checked);
  //     },
  //   },
};
</script>

<style scoped>
/*footer*/
.todo-footer {
  height: 40px;
  line-height: 40px;
  padding-left: 6px;
  margin-top: 5px;
}

.todo-footer label {
  display: inline-block;
  margin-right: 20px;
  cursor: pointer;
}

.todo-footer label input {
  position: relative;
  top: -1px;
  vertical-align: middle;
  margin-right: 5px;
}

.todo-footer button {
  float: right;
  margin-top: 5px;
}
</style>