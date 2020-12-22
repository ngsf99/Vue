<template lang="html">
  <div class="">
    <form @submit="addTodo">
      <input type="text" v-model="title" name="title" placeholder="AddTodo..">
      <input type="submit" name="Submit" class="btn">
    </form>
  </div>
</template>

<script>
//import {v4 as uuidv4} from 'uuid'; //jsonplaceholder has id so uuid becomes unnecssary

export default {
  name:"AddTodo",
  data(){
    return {
      title:''
    }
  },
  methods:{
    addTodo(e){
      e.preventDefault(); //prevent no changes during submit
      const newTodo = {
        //npm i uuid
  //    id: uuidv4(), //jsonplaceholder has id so uuid becomes unnecssary 
        title: this.title,
        completed: false
      }
      // send up to parent
      this.$emit('add-todo',newTodo);

      this.title = ''; //removing the typed words in the box
    }
  }
}
</script>

<style lang="css" scoped>
  form{
    display: flex;
  }

  input[type="text"]{
    flex:10;
    padding: 5px;
  }

  input[type="submit"]{
    flex:2;
  }

</style>
