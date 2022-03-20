<template>
  <!-- <createTL :newCategory="newCategory" :categories="categories" /> --> 

  <!--Add new Category-->
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
/*import createTL from './components/createTL.vue'*/

export default {
  name: "App",
  components: {
    boxTL /*createTL*/,
  },
  data() {
    return {
      //newTask: "",
      cTasks: [{ id: 1, name: "herbert" }], 
      newTL:"",
      tasklists: [{id:1, 
                  newTask: "",
                  categoryName:"hello", 
                  tasks:[{id:1, name: "hello"}]}]
    };
  },
  methods: {
    //if boxTL.id 
  //Save new Task in Tasks Array 
  submitTask: function submitTask(id) {
    for 
    if(this.tasklists.newTask=="") return;
    let new_id = this.tasklist.tasks.slice(-1)[0].id + 1;
   //  console.log(this.newTask);
     this.tasklist.tasks.push({
        id: new_id,
        name: this.tasklist.newTask,
       

      });
      this.tasklists.newTask="";
    }

    
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

  
}
}
</script> 

<style>
</style>
