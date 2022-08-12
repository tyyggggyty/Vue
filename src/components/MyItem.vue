<template>
  <li>
    <label>
      <input
        :checked="todo.done"
        type="checkbox"
        @click="handleCheck(todo.id)"
      />
      <span v-show="!todo.isEdit">{{ todo.title }}</span>
      <input v-show="todo.isEdit" type="text" :value="todo.title" @blur="handleUpdate(todo,$event)" ref="inputTitle">
    </label>
    <button class="btn btn-danger" @click="handleDelete(todo.id)">删除</button>
    <button class="btn btn-edit" @click="handleEdit(todo)">编辑</button>
  </li>
</template>

<script>
export default {
  name: "MyItem",
  props: ["todo"],
  methods: {
    handleCheck(id) {
      this.$bus.$emit("checkTodo", id);
    },

    handleDelete(id) {
      if (confirm("确认删除吗？")) this.$bus.$emit("deleteTodo", id);
    },
    handleEdit(todo) {
      this.$bus.$emit("editTodo", todo);
      this.$nextTick(function(){
        this.$refs.inputTitle.focus();
      })
    },
    handleUpdate(todo,e){
      this.$bus.$emit('updateTodo',todo,e.target.value)
    }
  },
};
</script>

<style scoped>
/*item*/
li {
  list-style: none;
  height: 36px;
  line-height: 36px;
  padding: 0 5px;
  border-bottom: 1px solid #ddd;
}

li label {
  float: left;
  cursor: pointer;
}

li label li input {
  vertical-align: middle;
  margin-right: 6px;
  position: relative;
  top: -1px;
}

li button {
  float: right;
  display: none;
  margin-top: 3px;
  margin-right: 5px;
  margin-left: 5px;
}

li:before {
  content: initial;
}

li:last-child {
  border-bottom: none;
}

li:hover {
  background-color: #ddd;
}

li:hover button {
  display: block;
}
</style>