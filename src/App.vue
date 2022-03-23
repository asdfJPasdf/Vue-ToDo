<template>
  <!-- <createTL :newCategory="newCategory" :categories="categories" /> 
  <boxTL v-for="category in categories" 
    :id="category.id" 
    :categoryName="category.name" 
    :tasks="category.tasks" 
    :key="category.id"
    :newTask="newTask"
  /> -->
  <!--new TL-->
   <div class= "d-flex">
        <input type="text" placeholder="Add new Tasklist" class="form-control-sm" v-model="newTL"  @keyup.enter="createTL">
        <button button class="btn  rounded-0" @click="createTL">create Tasklist</button> 
        <br>
    </div> 
  
 

  <!-- BoxTL component / assign Parameters-->    
 <boxTL v-for="tasklist in tasklists"  :key="tasklist.id"
  :id="tasklist.id"
  :newTask="newTask" 
  :categoryName="tasklist.categoryName" 
  :tasks="tasklist.tasks" @submitTask="submitTask"  
  :modelValue="tasklist.newTask" 
  @update:modelValue="tasklist.newTask = $event"/>
</template>


</template>

<script>
import boxTL from "./components/boxTL.vue";
import axios from "axios";
/*import createTL from './components/createTL.vue'*/

export default {
  name: "App",
  components: {
    boxTL /*createTL*/,
  },
  data() {
    return {
      newTask: "",
      NameCategory: "test",
      cTasks: [],
      categoryName: "Hallo",
      todo:"",
      categories: [],
      newCategory: "",
      
      newTL:"",
      tasklists: [{id:1, 
                  newTask: "",
                  categoryName:"hello", 
                  tasks:[{id:1, name: "hello"}]
                  }]


    };
  },
   async created() {
    try {
      const res = await axios.get(`http://localhost:3000/todos`);
      this.cTasks = res.data;
    } catch (error) {
      console.log(error);
    }
  },
  methods: {

  //Save new Task in Tasks Array 
 async submitTask() {
    let new_id;
    if(this.newTask=="") return;
    if(this.cTasks.lenght){
        new_id = this.cTasks.slice(-1)[0].id + 1;}
    else { new_id = 1; }
      const res = await axios.post(`http://localhost:3000/todos`, {
        id: new_id,
        name: this.newTask,
      });
      this.cTasks = [...this.cTasks, res.data];

     /*  
      this.cTasks.push({
        id: new_id,
        name: this.newTask,
        */
     },
     removeTask(id) {
    axios.delete(`http://localhost:3000/todos/${id}`)
    this.cTasks = this.cTasks.filter(cTasks => cTasks.id !== id)
    },

    createTL: function createTL() {
    if(this.newTL=="") return;
    let new_id = this.tasklists.slice(-1)[0].id + 1;
   //  console.log(this.newTask);
      this.tasklists.push({
        id: new_id,
        categoryName: this.newTL,
        tasks:[]
        
      });
      this.newTL = "";
   },

      
      

  },
   /*async addItem() {
      const res = await axios.post(`http://localhost:3000/todos`, {
        name: this.newTask,
      });
      this.cTasks = [...this.cTasks, res.data];
      this.newTask = "";
    },*/

  
}

</script> 

<style>
</style>
