<template>
  <ul class="todo-main">
    <Item v-for="todo of todoList" :key="todo.id"
          :todo="todo"
          :change-state="changeState"
          :remove-item="removeItem"/>
  </ul>
</template>


<script>
import Item from "@/components/Item.vue";

export default {
  name: 'List',
  components: {
    Item
  },
  props:['todoList','changeState','removeItem'],
  /*mounted() {
    console.log(this.todoList)
    console.log(this.changeState)
  }*/
}

</script>


<style scoped>
/*main*/
.todo-main {
  margin-left: 0;
  border: 1px solid #ddd;
  border-radius: 2px;
  padding: 0px;
}

.todo-empty {
  height: 40px;
  line-height: 40px;
  border: 1px solid #ddd;
  border-radius: 2px;
  padding-left: 5px;
  margin-top: 10px;
}
</style>