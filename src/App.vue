<template>
<div>
<div v-if="!isEditMode">
<form @submit.prevent="submitHandler" >
<input type='text' placeholder="Enter task" :value="title" @input="event => title = event.target.value">
<button type="submit" >Submit</button>

</form>
  
</div>
<div v-else>
  <h1>Edit form</h1>
  <form @submit.prevent="submitUpdateHandler" >
<input type='text' placeholder="Enter task" v-model="title">
<button type="submit" >Update</button>

</form>

</div>
 <TodoList v-bind:todoListItems="todoListItems"
  @delete-todo-event="deleteItem" @edit-todo-event="editItem"/>
</div>
</template>

<script>

import TodoList from './components/TodoList.vue'
import { v4 as uuidv4 } from 'uuid';

export default {
  name: 'App',
  components: {

    TodoList
    
  },
  data(){
    return{
       title:'',
      isEditMode:false,
      update:null,
      todoListItems: [
                {
                    id: 0,
                    title: 'clean house',
                    completed: false,
                   
              
                },
                {
                    id: 1,
                    title: 'watch Tv',
                    completed: false,
                   
                },
                {
                    id: 2,
                    title: 'wash the car',
                    completed: false,
                   
                },
                ],
    }

  },
  methods:{
    isEdit(){
       return this.isEditMode 
      // this.title = this.todoListItems.title
    },
  submitHandler(){
     
     const addItem={
      id:uuidv4(),
      title:this.title,
       completed: false
     }
     this.todoListItems=[...this.todoListItems,addItem]
    //  this.$emit("add-todo-event", addItem);
     this.title='';
     
    },
    submitUpdateHandler(){
          this.todoListItems[this.update].title=this.title
     
        // this.todoListItems.map((item)=>{
    
        //   if(item.id === this.update){
        //  this.todoListItems[this.update].title=this.title
          
        
        //   }
  
        // })
        // console.log("ff",this.todoListItems[this.update])
        // this.todoListItems[this.update].title= this.title;
        // this.update=null;
      // }
       this.isEditMode=false
       this.title='';
    },
  
    
deleteItem(toDoId){
  this.todoListItems=this.todoListItems.filter(item=> item.id !== toDoId)
  },
  editItem(todoId){
   
    this.update=todoId
  
    this.title = this.todoListItems[todoId].title;
    
    this.isEditMode = ! this.isEditMode
 
  },
  
}
  
  
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
