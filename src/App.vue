<template>
  <div id="root">
    <div class="todo-container">
      <div class="todo-wrap">
        <ToDoHeader :add-todo="addTodo"/>
        <List
            :todo-list="this.todoList"
            :change-state="changeState"
            :remove-item="removeItem"
        />
        <ToDoFooter :todoList="todoList" :checkAllTodo="checkAllTodo" :clearAllDone="clearAllDone"/>
      </div>
    </div>
  </div>
</template>

<script>
import ToDoHeader from "./components/ToDoHeader.vue";
import List from "./components/List.vue";
import ToDoFooter from "./components/ToDoFooter.vue";
import {nanoid} from "nanoid";

export default {
  name: 'App',
  components: {
    ToDoHeader,
    List,
    ToDoFooter
  },
  data() {
    return {
      todoList: [
        {id: '001', title: '起床', done: true},
        {id: '002', title: '洗漱', done: true},
        {id: '003', title: '上班', done: true},
        {id: '004', title: '吃午饭', done: false},
      ],

    }
  },
  methods: {
    // 添加一个todo事件
    addTodo(todoObj) {
      // 输入的转为todo对象加入到todoList中
      console.log(todoObj.target);

      this.todoList.unshift(todoObj);
    },
    // 更改todo事件完成状态
    changeState(todoId) {
      this.todoList.forEach(t => {
        if (t.id === todoId) {
          t.done = !t.done;
        }
      })
    },
    // 移除待办已办事项
    removeItem(todoId) {
      if (confirm("确认删除该事项吗？")) {
        this.todoList = this.todoList.filter(todo => todo.id !== todoId)
      }
    },
    // 全选/取消全选
    checkAllTodo(checked) {
      this.todoList.forEach(todo => todo.done = checked)
    },
    clearAllDone(){
      this.todoList = this.todoList.filter(todo => {
        return !todo.done
      })
    }
  }
}
</script>

<style>
/*base*/
body {
  background: #fff;
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
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.2), 0 1px 2px rgba(0, 0, 0, 0.05);
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
