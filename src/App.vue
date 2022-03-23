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
      categoryName: "Hallo",
      todo:"",
      categories: [],
      newCategory: "",
      
      newTL:"",
      tasklists: [[]]
                  


    };
  },
   async created() {
    try {
      const res = await axios.get(`http://localhost:3000/tasklists`);
      this.tasklists = res.data;
    } catch (error) {
      console.log(error);
    }
  },
  methods: {

  //Save new Task in Tasks Array 
 async submitTask() {
    let new_id;
    if(this.newTask=="") return;
    if(this.tasklists.lenght){
        new_id = this.tasklists.slice(-1)[0].id + 1;}
    else { new_id = 1; }
      const res = await axios.post(`http://localhost:3000/tasklists`, {
        id: new_id,
        name: this.newTask
      });
      this.tasklists = [...this.tasklists, res.data];

     /*  
      this.tasklists.push({
        id: new_id,
        name: this.newTask,
        */
     },
     removeTask(id) {
    axios.delete(`http://localhost:3000/tasklists/${id}`)
    this.tasklists = this.tasklists.filter(tasklists => tasklists.id !== id)
    },
 async createTL() {
    if(this.newTL=="") return;
    let new_id_box = this.tasklists.slice(-1)[0].id + 1;
   //  console.log(this.newTask);
     const res = await axios.post(`http://localhost:3000/tasklists`, {
        id: new_id_box,
        categoryName: this.newTL
      });
      this.tasklists = [...this.tasklists, res.data];
      this.newTL = "";
   },

      
      

  },
   /*async addItem() {
      const res = await axios.post(`http://localhost:3000/todos`, {
        name: this.newTask,
      });
      this.tasklists = [...this.tasklists, res.data];
      this.newTask = "";
    },*/

  
}

</script> 

<style>
</style>
