<template>
  <div id="app">
   
    <AddToDo v-bind:todos="todos" v-on:add-todo="addToDo"></AddToDo>
    <todos v-bind:todos="todos" v-on:del-todo="delToDo" />
  </div>
</template>

<script>
import Todos from "../components/Todos";

import AddToDo from "../components/AddToDo";
import axios from "axios";

export default {
  name: "Home",
  components: {
    Todos,
    AddToDo,
  },
  methods: {
    delToDo(id) {
      axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
      .then(res =>{
        console.log(res)
         this.todos=this.todos.filter(todo=>todo.id!=id)}) 
        .catch((error) => console.error(error));
      
    },
    addToDo(newToDo) {
      const { title, completed } = newToDo;
      console.log(newToDo)
      axios
        .post("https://jsonplaceholder.typicode.com/todos",{
          title,
          completed
        })
        .then(res =>{console.log(res)
         this.todos=[...this.todos,res.data]}) 
        .catch((error) => console.error(error));
    },
  },
  created() {
    //its like component didmount of react it works after component loads
    axios
      .get("https://jsonplaceholder.typicode.com/todos?_limit=10")
      .then((res) => (this.todos = res.data))
      .catch((error) => console.error(error));
  },
  data() {
    return {
      todos: []
    };
  },
};
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body {
  font-family: Arial, Helvetica, sans-serif;
  line-height: 1.4;
}
.btn {
  display: inline-block;
  border: none;
  background: #555;
  color: #fff;
  padding: 7px 20px;
  cursor: pointer;
}
.btn:hover {
  background: #666;
}
</style>
