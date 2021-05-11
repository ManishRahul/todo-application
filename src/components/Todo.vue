<template>
  <div>
    <!-- <form @submit="submitForm"> -->
      <div>
        <label>Enter a title : </label><br />
        <input type="text" v-model="title" /> <br /><br />
      </div>

      <div>
        <label>Type in your todos :</label><br />

        <input type="text" v-model="todo" required />
        <button v-on:click="addtodo" > Add</button>
      </div>
      <br />
      <div>
        <button @click="addTitle_and_Todo"> OK </button>
      </div>
      <div>
        <button @click="displayElement"> Display </button>
      </div>
    <!-- </form> -->

    <!-- <ol style="list-style: none">
      <li v-for="item in tasks" :key="item">{{item}}</li>
    </ol> -->

    
    <div v-for="x in todos" :key="x.title">   
      <h4>{{ x.title }}</h4>
      <div v-for="y in x.tasks" :key="y.todo">   
        <h4>{{ y.todo }}</h4>
      </div>
    </div>
    <br />
    <!-- v-bind:id="design" -->


    <div style="padding-top: 100px; padding-left: 50px" >
      <h3>Your todo list :</h3>
    </div>
  </div>
</template>
<script>
export default {
// Vue.mixin({
//   data:function(){
//     return{
//       num : "hello"
//     }
//   }
// }),

  name: "Todo",
  data() {
    return {
  
      title: " ",

      todo: " ",
      copytodo: " ", // this variable copys the todo value
      tasks:[], // on clicking Add button, todo will get inserted

      todos: [
        [  

          // onclicking the 'OK' button, title and tasks[] will get inserted here

        ],
      ],
    };
  },

  methods: {
    addtodo() { // this executes when Add button is clicked
      this.tasks.push(this.todo)
      console.log(this.tasks)

    },
    
    addTitle_and_Todo() { // this executes when 'OK' button is clicked
     
      this.todos.push([this.title,this.tasks]) //this syntax worked as expected
      this.tasks = []
      console.log(this.todos)
      
    },


    displayElement(){
      console.log(this.todos[4])
    }
  },
};
</script>
<style>
#designcss {
  height: 100%;
  width: 50%;
  position: fixed;
  z-index: 1;
  top: 0;
  overflow-x: hidden;
  padding-top: 20px;
  right: 0;
  border-left: 4px solid #4a6566;
  height: 550px;
}
</style>