<template>
  <div class="page-container">
    <md-toolbar class="md-accent">
      <h3 class="md-display-1">To Do List App</h3>
    </md-toolbar>
    <md-field>
      <md-input v-model="currentTodo" @keydown.enter="addTodo()" placeholder="Add a todo" maxlength="70"></md-input>
      <md-button class="md-fab md-accent" @click="addTodo()">
        <md-icon>add</md-icon>
      </md-button>
    </md-field>
    <md-toolbar class="md-transparent todo-list">
      <h3 class="md-title">To Do or Not To Do :)</h3>
      <ul class="todos">
        <li v-for="todo in todos" :key="todo.id">
          <span @dblclick="clickToEdit(todo)" v-show="editTodoId !== todo.id" :class="{ completed: todo.completed }">{{ todo.label }}</span>
          <input class="editingToDo" v-on:click.stop.prevent v-model="todo.label" v-show="editTodoId == todo.id" v-on:keyup.enter="saveEdit">
          <span class="flexEnd">
            <md-checkbox type="checkbox" v-model="todo.completed"></md-checkbox>
            <md-button class="md-accent" @click="removeToDo(todo)">Remove</md-button>
            <md-button class="md-accent md-dense" @click="clickToEdit(todo)">
              <md-icon class="editIcon">edit</md-icon>
            </md-button>
          </span>
        </li>
      </ul>
    </md-toolbar>
  </div>
</template>

<script>
export default {
 name: 'RegularToolbar',
  data() {
    return {
      todos: [],
      currentTodo: '',
      editTodoId: null
    };
  },
  methods: {

    addTodo() {
      if(this.currentTodo !== ''){
        this.todos.push({id: this.todos.length, label: this.currentTodo, completed: false});
      this.currentTodo = '';
      }
      else{
        alert("No Way :) Please enter to do task !!!");
      }
    },

    removeToDo(todo){
      const index = this.todos.indexOf(todo);
      this.todos.splice(index, 1);
    },

    clickToEdit(todo) {
      this.editTodoId = todo.id; 
    },

    saveEdit(){
      this.editTodoId = null;
    }
  }
};
</script>

<style scoped >

  .page-container{
    display: flex;
    justify-content: center;
    flex-direction: column;
    align-items: center;
   } 

  .md-display-1{
    padding: 1rem;
  }

   .md-field{
    display: flex;
    width: 70vw;
    padding: 1rem;
    margin: 1rem;
  }

  .todo-list{
    display: flex;
    justify-content: flex-start;
    width: 70vw;
    margin-top: 1rem;
  }

  .md-title{
    color: #BCC1B8!important;
    margin-top: 1rem!important;
  }

  ul{
    display: flex;
    flex-direction: column;
    margin-left: 0 ;
    width: 100%;
    padding-inline-start: 0px!important;
  }

  li{
    display: flex;
    justify-content: space-between;
    align-items: center;
    width: 100%;
    border: 2px solid #ff5252;
    border-radius: 0.5rem;
    margin-bottom: 0.5rem;
    margin-right: 0;
    padding-left: 1rem;
    position: relative;
  }

  .flexEnd{
    margin-left: auto;
  }

  .completed{
    color: rgba(248, 239, 239, .3);
  }

  .completed::after{
    content: " Completed";
    text-decoration: none;
    font-weight: bolder;
    color: #ff5252;
    background: rgb(209, 208, 208);
    padding: .3rem;
    margin-left: 2rem;
    border-radius: 0.3rem;
  }

  .editIcon{
    color: #ff5252!important;
  }

  .editingToDo{
    padding: .3rem;
    border:0;
    box-shadow:0 0 15px 4px rgba(0,0,0,0.06);
    background: #f3dbdb;
    color: rgba(0,0,0, 0.8);
    font-weight: bolder;
    
  }

  .editingToDo:focus {
    box-shadow: 0 0 10px rgb(209, 208, 208);
  }

  input.editingToDo:focus + *::before {
    content: "After editing, press 'ENTER' to save the changes.";
    position: absolute;
    right: 40%;
    bottom: 100%;
    color: #ff5252;;
    font-size: 1rem;
    background: rgba(0,0,0, 0.5);
    padding: 0.8rem;
    margin: 0.5rem;
    border-radius: 0.3rem;
  }
  
</style>