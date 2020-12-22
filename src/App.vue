<template lang="html">
  <div id="app">
    <Header />
    <AddTodo v-on:add-todo="addTodo" />
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo" />
  </div>
</template>

<script>
import Todos from './components/Todos.vue';
import Header from './components/layout/Header.vue';
import AddTodo from './components/AddTodo.vue';
import axios from 'axios';

export default {
  name:'app',
  components:{
    Header,
    Todos,
    AddTodo
  },
  data(){
    return {
      todos:[]
    }
  },
  methods:{
    deleteTodo(id){
//      axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`)  //delete from serve and request for url
//        .then(res => this.todos = this.todos.filter(todo => todo.id !== id))
//        .catch(err => console.log(err));
      this.todos = this.todos.filter(todo => todo.id !== id); //not working for axios
    },
    addTodo(newTodo){ //submit and request to url
      const{ title , completed } = newTodo;
      //promises
      axios.post('https://jsonplaceholder.typicode.com/todos',{
        title,
        completed
      })
        .then(res => this.todos = [...this.todos, res.data])
        .catch(err => console.log(err));

//    this.todos = [...this.todos, newTodo]; //with jsonplaceholder(backend)
    }
  },
  created(){ // submit to our page
    //npm i axios
    axios.get('https://jsonplaceholder.typicode.com/todos?_limit=10') //url?_limit=10
      .then(res => this.todos = res.data) // the page data will transfter to our data's todos
      .catch(err => console.log(err));
  }
}
</script>

<style lang="css" scoped>
  *{
    box-sizing: border-box;
    margin: 0;
    padding: 0;
  }
  .btn{
    display: inline-block;
    border:none;
    background: #555;
    padding:7px 20px;
    cursor:pointer;
  }

  .btn:hover{
    background: #666;
  }

</style>
