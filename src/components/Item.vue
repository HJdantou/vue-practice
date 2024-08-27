<template>
  <li>
    <label>
      <!--      这里勾选和取消勾选可以使用change和click作为事件处理,勾选需要将todoList中的数据状态改了-->
<!--      <input type="checkbox" :checked="todo.done" v-on:click="handleCheck(todo.id)"/>-->
      <input type="checkbox" :checked="todo.done" v-on:change="handleCheck(todo.id)"/>
      <!--v-model数据的双向绑定，checkbox使用v-model来双向绑定其是否被勾选,也可以实现效果但不推荐(因为其实修改了props中的数据)-->
      <!--这里修改了从List修改过来的props,这里的不允许改是浅层次，就是如果props是一个对象则这个修改这个对象的某一个属性vue是放行的-->
      <!-- <input type="checkbox" v-model="todo.done"/>-->
      <span>{{ this.todo.title }}</span>
    </label>
    <button class="btn btn-danger" v-on:click="deleteItem(todo.id)">删除</button>
  </li>
</template>


<script>

export default {
  name: 'Item',
  props: ['todo', 'changeState','removeItem'],
  /*mounted() {
    console.log(this.todo)
    console.log(this.changeState)
  },*/
  methods: {
    handleCheck(todoId) {
      // 通知App组件把对应数据done值取反
      this.changeState(todoId)
    },
    // 删除待办已办事
    deleteItem(todoId){
      // 通知App组件删除对应todo事件
      this.removeItem(todoId)
    }
  }
}

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
}

li:before {
  content: initial;
}

li:last-child {
  border-bottom: none;
}

li:hover {
  background: #dddddd;
}

li:hover button {
  display: block;
}
</style>