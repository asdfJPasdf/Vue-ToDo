<template>
   <createTL :newCategory="newCategory" :categories="categories" /> 
  <boxTL v-for="tasklist in tasklists" 
    :id="tasklist.id" 
    :categoryName="tasklist.name" 
    :tasks="tasklists.tasks" 
    :key="tasklist.id"
    
  /> 
  <!--Add new Category-->
  <div class= "d-flex">
        <input type="text" placeholder="Add new Tasklist" class="form-control-sm" v-model="newTL"  @keyup.enter="createTL">
        <button button class="btn  rounded-0" @click="createTL">create Tasklist</button> 
        <br>
    </div> 
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
      cTasks: [{ id: 1, name: "hans" }], 
      newCategory:"",
      tasklists: [{id:1, 
                  categoryName:"Test", 
                  tasks:[this.cTasks]}]
    };
  },
  methods: {

  //Save new Task in Tasks Array 
  submitTask: function submitTask() {
    if(this.newTask=="") return;
    let new_id = this.cTasks.slice(-1)[0].id + 1;
   //  console.log(this.newTask);
      this.cTasks.push({
        id: new_id,
        name: this.newTask,
      });
      this.newTask = "";
   },
   createTL: function createTL() {
    if(this.newCategory=="") return;
    let new_id = this.cTasks.slice(-1)[0].id + 1;
   //  console.log(this.newTask);
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
