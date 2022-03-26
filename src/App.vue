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
        <input type="text" placeholder="Add new Tasklist" class="form-control-sm" v-model="newTL"  @keyup.enter="submitCategories">
        <button button class="btn btn-dark" @click="submitCategories">create Tasklist</button> 
        <br>
    </div> 
  <boxTL v-for="categorie in categories "  :key="categorie.id"
  :id="categorie.id"
  :newCategory="newCategory" 
  :categoryName="categorie.categoryName" 
  :tasks="categorie.tasks" @submitTask="submitTask"  
  :modelValue="categorie.newTask" 
  @update:modelValue="categorie.newCategory = $event"/>
 

  <!-- BoxTL component / assign Parameters-->    
 
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
      tasks:[],
      newCategory: "",  
      newTL:"",
      
                  


    };
  },
   async createdCategories() {
    try {
      const res = await axios.get(`http://localhost:3000/categories`);
      this.categories = res.data;
    } catch (error) {
      console.log(error);
    }
  },
   async createdTask() {
    try {
      const res = await axios.get(`http://localhost:3000/task`);
      this.categories = res.data;
    } catch (error) {
      console.log(error);
    }
  },
  methods: {

  //Save new Task in Tasks Array 
 async submitTask(id) {
    let new_id;
    if(this.newTask=="") return;
    if(this.tasklists.lenght){
        new_id = this.tasklists.slice(-1)[0].id + 1;}
    else { new_id = 1; }
      const res = await axios.post(`http://localhost:3000/tasks`, {
        id: new_id,
        name: this.newCategory,
        categoryId: id
      });
      this.task = [...this.task, res.data];

     /*  
      this.tasklists.push({
        id: new_id,
        name: this.newTask,
        */
     },
     async submitCategories(id) {
    let new_id;
    if(this.newCategory=="") return;
    if(this.categories.lenght){
        new_id = this.categories.slice(-1)[0].id + 1;}
    else { new_id = 1; }
      const res = await axios.post(`http://localhost:3000/categories`, {
        id: new_id,
        name: this.newCategory,
        categoryId: id
      });
      this.task = [...this.task, res.data];
     },
     removeTask(id) {
    axios.delete(`http://localhost:3000/tasklists/${id}`)
    this.tasklists = this.tasklists.filter(tasklists => tasklists.id !== id)
    },
 /*async createTL() {
    if(this.newTL=="") return;
    let new_id_box = this.tasklists.slice(-1)[0].id + 1;
   //  console.log(this.newTask);
     const res = await axios.post(`http://localhost:3000/categories`, {
        id: new_id_box,
        categoryName: this.newTL
      });
      this.tasklists = [...this.tasklists, res.data];
      this.newTL = "";
   },*/

      
      

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
