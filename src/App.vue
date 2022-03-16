<template>
  <!-- <createTL :newCategory="newCategory" :categories="categories" /> 
  <boxTL v-for="category in categories" 
    :id="category.id" 
    :categoryName="category.name" 
    :tasks="category.tasks" 
    :key="category.id"
    :newTask="newTask"
  /> -->
    <div class="d-flex">
      <input type="text" placeholder="Add Task..." class="form-control-sm" v-on:keyup.enter="submitTask" v-model="newTask" />
      <button class="btn rounded-0" @click="submitTask">SUBMIT</button>
      <br />
    </div>    
  <boxTL
  :newTask="newTask" 
  :categoryName="NameCategory" 
  :tasks="cTasks" @submitTask="submitTask"/>
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
  async submitTask() {
    if(this.newTask=="") return;
     console.log(this.newTask);
    let new_id = this.cTasks.slice(-1)[0].id + 1;
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
}
      
      
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
