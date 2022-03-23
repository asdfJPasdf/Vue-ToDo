<template>
  <!-- <createTL :newCategory="newCategory" :categories="categories" /> 
  <boxTL v-for="category in categories" 
    :id="category.id" 
    :categoryName="category.name" 
    :tasks="category.tasks" 
    :key="category.id"
    :newTask="newTask"
  /> -->
  
  <!-- BoxTL component / assign Parameters-->    
  <boxTL
  :newTask="newTask" 
  :categoryName="NameCategory" 
  :tasks="cTasks" @submitTask="submitTask"  
  :modelValue="newTask" 
  @update:modelValue="newTask = $event"/>
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
      cTasks: [], 
    
    };
  },
  methods: {

  //Save new Task in Tasks Array 
  submitTask: function submitTask() {
    let new_id;
    if(this.newTask=="") return;
    if(this.cTasks.lenght){
        new_id = this.cTasks.slice(-1)[0].id + 1;}
    else { new_id = 1; }
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
