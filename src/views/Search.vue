<template>
<h1>Search</h1>
    <div class= "d-flex justify-content-center" style="position:absolute top:5px" >
     <center>        <input type="text" placeholder="Search.." class="form-control-sm" v-model="searchTerm"  @keyup.enter="submitCategories">
        <button button class="btn btn-dark" @click="searchTask">search</button> 
        <br>
        </center>

    </div> 
</template>

<script>
import axios from "axios";
export default {
   name: "Search",
  components: {
    
  },
  data() {
    return {
       tasks:[],
       searchTerm: "",
       title:"",
       Done: false


    };
  },
   async created() {
    try {
      const resCategories = await axios.get(`http://localhost:3000/categories`);
      this.categories = resCategories.data;
    } catch (error) {
      console.log(error);
    }
    
    try {
      const resTasks = await axios.get(`http://localhost:3000/tasks`);
      this.tasks = resTasks.data;
    } catch (error) {
      console.log(error);
    }
  },
  
  methods: {

    findTask(searchTerm,tasks){
    this.Done = tasks.find(findTask).Done;
    this.title = tasks.find(findTask).taskName;
    function findTask(tasks)
    {
    return tasks.taskName===searchTerm;
    }
console.log(this.title)
  }
  }


}
</script>

<style>

</style>