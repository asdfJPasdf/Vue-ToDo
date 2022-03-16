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
      cTasks: [{ id: 1, name: "hans" }],
      categoryName: "Hallo",

      categories: [],
      newCategory: "",

    };
  },
   async created() {
    try {
      const res = await axios.get(`http://localhost:3000/todos`);
      this.items = res.data;
    } catch (error) {
      console.log(error);
    }
  },
  methods: {
  submitTask: function submitTask() {
    if(this.newTask=="") return;
     console.log(this.newTask);
       let new_id = this.cTasks.slice(-1)[0].id + 1;
      this.cTasks.push({
        id: new_id,
        name: this.newTask,
        
      });
      this.newTask = "";
      
  },

  
}
}
</script> 

<style>
</style>
