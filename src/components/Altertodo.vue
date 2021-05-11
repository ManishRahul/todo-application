<template>
  <div id="bg">
    <form @submit="addTitle_and_Todo">
      <div style="padding-top: 30px; padding-left: 30px" id="leftlayout">
        <h1>Todo List App</h1><br><br>
        <div>
          <label>Enter a title : </label><br />
          <input type="text" v-model="title" required /> <br /><br />
        </div>

        <div v-if="!isEditing">
          <label>Type in your todos :</label><br />
          <input type="text" v-model="todo" />
          <button  v-on:click="addtodo" style="margin-left:10px" class="btn btn-info" type="button">Add</button>
        </div>
        <div v-else>
          <label>You can edit the todo :</label><br />
          <input type="text" v-model="todo" />
          <button  v-on:click="updateTodo" style="margin-left:10px" class="btn btn-info" type="button">Update</button>
        </div>

        <br />
        <ol style="list-style: none">
          <li v-for="(item, index) in tasks" :key="item">
            {{ index + 1 }} {{ item }}
          </li>
        </ol>
        <div>
          <button type="submit" value="OK" class="btn btn-success" > OK </button>
        </div>
      </div>
    </form>

    <div style="padding-top: 60px" id="rightlayout">
      <h2 style="padding-left: 30px"><u>Your todo list :</u></h2>
      <div  v-bind:id="isTodoAdded && 'list'">
        <div v-for="(x,index) in todos" :key="x.title">
          <h4 style="padding-left: 20px"><u>{{ x.title }}</u></h4>
          <ul
            v-for="(y, innerindex) in x.tasks"
            :key="y.innerindex"
          >
            <li>{{ x.tasks[innerindex] }}
            <span @click="edit_Todo(index,innerindex,y)"><i class="fa fa-pencil" aria-hidden="true"></i></span>
            <span @click="delete_Todo(index,innerindex)"><i class="fa fa-trash" aria-hidden="true"></i></span>
            </li>
          </ul>
        </div>
      </div>
    </div>
    <!-- v-bind:id="design" -->
  </div>
</template>
<script>
export default {
  name: "Altertodo",
  data() {
    return {
      title: "",

      todo: "",
      copytodo: "", // this variable copys the todo value
      tasks: [], // on clicking Add button, todo will get inserted

      todos: [
        {
          // onclicking the 'OK' button, title and tasks[] will get inserted here
        },
      ],
      design: "designcss",
      isTodoAdded : false, // the todo textbox should be filled, else it won't get added
      isTodoFilled : false, // 
      isTitleFilled : false,

      isEditing : false,
      selectedIndex : null
    };
  },

  methods: {
    addtodo() {
      // this executes when Add button is clicked
      if(this.todo==""){
        alert("Enter a todo")
        
      }
      else
      {
      this.tasks.push(this.todo);
      this.todo = "";
      console.log(this.tasks);
      this.isTodoFilled = true
      }
    },

    addTitle_and_Todo() {
      // this executes when 'OK' button is clicked
      event.preventDefault();

      if(this.isTodoFilled && this.title != null){
      this.todos.push({ title: this.title, tasks: this.tasks }); //this syntax worked as expected
      this.tasks = [];
      console.log(this.todos);
      this.title = "";
      
      this.isTodoAdded = true
      this.isTodoFilled = false
      }
      else{
        alert("Atleast one todo should be added")
      }

    },

    edit_Todo(index,innerindex,y){
        this.todo = y
        this.isEditing = true
        this.selectedIndex = index
        this.selectedInnerIndex = innerindex
    },

    updateTodo()
    {
      if(this.todo != ""){
      this.todos[this.selectedIndex].tasks[this.selectedInnerIndex] = this.todo
      this.todo = ""
      this.isEditing = false
      }
      else{
        alert("no todo exist, please enter one")
      }

    },

    delete_Todo(index, innerindex){ //this is to delete
        this.todos[index].tasks.splice(innerindex, 1)
    },
  },
};
</script>
<style>


#leftlayout {
  height: 100%;
  width: 50%;
  position: fixed;
  z-index: 1;
  top: 0;
  overflow-x: hidden;
  padding: 20px 0px 0px 20px;
  
  text-align : left;
  left: 0;
  height: 550px;
}

#rightlayout {
  height: 100%;
  width: 50%;
  position: fixed;
  z-index: 1;
  top: 0;
  overflow-x: hidden;
  padding-top: 20px;
  
  text-align : left;
  right: 0;
  border-left: 4px solid #4a6566;
  height: 550px;
}
 #list{
   border : 1px solid;
   border-radius : 25px;
   /* height : 50%; */
   margin : 25px;
   text-align : left;
   /* padding : 30px; */
   overflow-wrap : break-word;
 }

 h1,h2{
   color:#c7188d!important;
   -webkit-text-stroke-width:2px;
   -webkit-text-stroke-color:#6d1515;
 }

 span{
   margin : 5px;
 }
</style>