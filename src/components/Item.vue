<template>
<div v-bind:class="{'completed':todo.completed}">
  <p @click="markCompleted"> {{todo.title}} </p>
  <button @click="$emit('delete-todo-event',todo.id)">Delete</button>
  <button @click="$emit('edit-todo-event',todo.id)">Edit</button>
  </div>
</template>

<script>

export default {
  name:"TodoItems",


props:[
  "todoItem"
],
data(){
return{
   todo:this.todoItem
}
},
methods:{
  markCompleted(){
    this.todo.completed =! this.todo.completed
  },
 
}
}
</script>
<style>
.completed {
        text-decoration: line-through;
      }
</style>