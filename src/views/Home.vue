<template>
<div :class="{isDarkmode:darkmode}">
  <!-- <createTL :newCategory="newCategory" :categories="categories" /> 
  <boxTL v-for="category in categories" 
    :id="category.id" 
    :categoryName="category.name" 
    :tasks="category.tasks" 
    :key="category.id"
    :newTask="newTask"
  /> -->
  <!--new TL-->
<h1>Vue-ToDo</h1>

   <div class= "d-flex justify-content-center" style="position:absolute top:5px" >
     <center>        <input type="text" placeholder="Add new Tasklist" class="form-control-sm" v-model="newCategory"  @keyup.enter="submitCategories">
        <button button class="btn btn-dark" @click="submitCategories">create Tasklist</button> 
        <br>
        </center>

    </div> 
    <div class= "position-absolute top-1 end-0" >
       <input type="text" placeholder="Search.." class="form-control-sm" v-model="searchTerm"  @keyup.enter="submitCategories">
        <!--<button button class="btn btn-dark" @click="searchTask">search</button> -->
        <br> 
    </div> 

    <button button class="btn btn-dark" @click="darkmode = !darkmode">{{darkmode ? "Lightmode" : "Darkmode"}}</button> 

  <!-- BoxTL component / assign Parameters-->    
   <boxTL v-for="categorie in categories "  :key="categorie.id"
  :id="categorie.id"
  :newCategory="newCategory" 
  :categoryName="categorie.categoryName" 
  :tasks="tasks" @submitTask="submitTask"  
  @removeTask="removeTask(tasks.id)"
  v-model="categorie.newTask"
  
  @update:modelValue="categorie.newCategory = $event"/>
  </div>
</template>




<script>
import boxTL from "../components/boxTL.vue";
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
      categories: [],
      tasks:[],
      newCategory: "",  
      newTL:"",
      searchTerm: "",
      darkmode: false


        //nicht verwendet
     // NameCategory: "test",
     // categoryName: "Hallo",
     // todo:"",
      
                  


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

  //Save new Task in Tasks Array 
 async submitTask(id) {
    let new_id;
    
    const index = this.categories.findIndex(item => item.id === id);

    
    console.log(this.newTask);
    if(this.categories[index].newTask =="")
    {
    this.$toast.show(`You cannot add an empty trask!`,{
        type:"error",
        position:'top-right',
        duration:3000,

      });
      return 

}
   if(this.categories.lenght==0){
        new_id=1;
        }
   else if (this.categories.lenght>0) { new_id = this.categories.slice(-1)[0].id + 1;}
      const res = await axios.post(`http://localhost:3000/tasks`, {
        id: new_id,
        taskName: this.categories[index].newTask ,
        categoryId: id,
        status: false
      });
      this.categories[index].newTask = "";
      this.tasks = [...this.tasks, res.data];
      


     /*  
      this.tasklists.push({
        id: new_id,
        name: this.newTask,
        */
     },



   async submitCategories() { 
      
    if(this.newCategory==="") {
      this.$toast.show(`You must give the category a name!`,{
        type:"error",
        position:'top-right',
        duration:3000,

      });
    
     
    }
    else{
   let new_id; 
    if(this.categories.lenght==0){
        new_id=1;
        }
   else if (this.categories.lenght>0) { new_id = this.categories.slice(-1)[0].id + 1;}
    
      const res = await axios.post(`http://localhost:3000/categories`, {
        id: new_id,
        categoryName: this.newCategory,
        newTask: ""
      });
       
      this.categories = [...this.categories, res.data];

      this.newCategory="";
      
    }
     },


    removeTask(id) {
    axios.delete(`http://localhost:3000/tasklists/${id}`)
    this.tasks = this.tasks.filter(tasks => tasks.id !== id)
    },
    /*
 async createTL() {
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
  computed: {
  filtered_Tasks() {

			if (this.search_text) {

				// Return a filtered array
				return this.tasks.filter(task => {
					
					// Set filter by check every word of search text
					return this.searchTerm
							.toLowerCase()
							.split(' ')
							.every(word => {
								return 	task.taskName.toLowerCase().includes(word)
										|| 
										task.done.toString().includes(word)
										|| 
										task.categoryName.toString().toLowerCase().includes(word)
							});
				});

			}
			else {
				return this.tasks;
			}
		
		},
   /*async addItem() {
      const res = await axios.post(`http://localhost:3000/todos`, {
        name: this.newTask,
      });
      this.tasklists = [...this.tasklists, res.data];
      this.newTask = "";
    },*/

  
}
}

</script> 

<style>


.isDarkmode * {
  background-color: rgb(42, 42, 42);
    color: white;
    
}
tbody *{
  text-align: left;
}
.isChecked{ 
  text-decoration: line-through
}
</style>
