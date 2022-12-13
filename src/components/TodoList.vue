<template>
<div> To Do List
  <ul>
    <li v-bind:key="item.id" v-for="item in todoListItems">
<TodoItem v-bind:todoItem="item" @delete-todo-event="$emit('delete-todo-event',item.id)"
@edit-todo-event="$emit('edit-todo-event',item.id)"
/>
</li>
</ul>
</div>
</template>

<script>
import TodoItem from './Item.vue';

export default {
  name:"TodoList",
  components: {

    TodoItem
    
  },
  props: [
    "todoListItems"
  ]

}
</script>
<style>
li{
   list-style-type: none;
}
</style>