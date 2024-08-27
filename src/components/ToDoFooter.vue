<template>
  <!--隐式类型转换-->
  <div class="todo-footer" v-show="total">
    <label>
      <!--这里也可用v-model来替代，此时不需要计算属性了-->
      <!--      <input type="checkbox" :checked="isAll" @change="checkAll"/>-->
<!--      <input type="checkbox" :checked="isAll" @change="checkAll"/>-->
      <input type="checkbox" v-model="isAll"/>
    </label>
    <span>
       <span>已完成{{ doneTotal }}</span> / 全部{{ total }}
    </span>
    <button class="btn btn-danger" v-on:click="clearAll">清除已完成任务</button>
  </div>
</template>


<script>

export default {
  name: 'ToDoFooter',
  props: ['todoList', 'checkAllTodo','clearAllDone'],
  data() {
    return {
      doneList: []
    }
  },
  computed: {
    total() {
      return this.todoList.length
    },
    doneTotal() {
      // filter写法
      /*this.doneList = this.todoList.filter(todo => todo.done)
      console.log(this.doneList)
      return this.doneList.length;*/
      // reduce写法
      return this.todoList.reduce((pre, current) => {
        /*console.log(pre)
        console.log(current)*/
        return pre + (current.done ? 1 : 0);
      }, 0)
    },
    // 使用计算属性时写简写
    /*isAll() {
      return this.total === this.doneTotal && this.total > 0;
    }*/
    // 用v-model实现是否全选中，完整写法
    isAll:{
      get(){
        return this.total === this.doneTotal && this.total > 0;
      },
      set(value){
        this.checkAllTodo(value)
      }
    }
  },
  methods: {
    checkAll(e) {
      // 通知App组件所有事项改为勾选完成
      this.checkAllTodo(e.target.checked)
    },
    // 清楚全部已完成事项
    clearAll(){
      // 通知App组件清除全部已完成事项
      this.clearAllDone();
    }
  }
}

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