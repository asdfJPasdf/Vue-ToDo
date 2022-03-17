<template>
  <!-- <createTL :newCategory="newCategory" :categories="categories" /> 
  <boxTL v-for="category in categories" 
    :id="category.id" 
    :categoryName="category.name" 
    :tasks="category.tasks" 
    :key="category.id"
    :newTask="newTask"
  /> -->
      
  <boxTL
  :newTask="newTask" 
  :categoryName="NameCategory" 
  :tasks="cTasks" @submitTask="submitTask" v-model="tTtext"/>
</template>

<script>
import boxTL from "./components/boxTL.vue";
/*import createTL from './components/createTL.vue'*/

export default {
  name: "App",
  components: {
    boxTL /*createTL*/,
  },
  data() {
    return {
      newTask: "",
      tTtext: "",
      NameCategory: "",
      cTasks: [{ id: 1, name: "hans" }],
      categoryName: "Hallo",

      categories: [],
      newCategory: "",

    };
  },
  methods: {
  submitTask: function submitTask() {
    //if(this.newTask=="") return;
     console.log(this.tTtext);
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
