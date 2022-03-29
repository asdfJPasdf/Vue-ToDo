<!--<template>
<h1>Categorie</h1>
    <div class= "d-flex justify-content-center" style="position:absolute top:5px" >
     <input type="text" placeholder="Search.." class="form-control-sm" v-model="searchTerm" >
        <br>
    </div>
  <div  v-if="filtered_Categorie.length">
    <div v-for="categorie in filtered_Categorie "  :key="categorie.id">
   <boxTL 
  :id="categorie.id"
  :newCategory="newCategory" 
  :categoryName="categorie.categoryName" 
  :tasks="tasks" />
 </div>
  </div>
   <p v-else class="mt-2">
			It doesn't exist a categorie with this name
		</p>
    
   
</template>

<script>
import boxTL from "../components/boxTL.vue";
import axios from "axios";
export default {
   name: "Categorie",
  components: {
    boxTL
  },
  data() {
    return {
       categories:[],
       searchTerm: "",
      
       


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
  
 computed: {
  filtered_Categorie() {

			if (this.searchTerm) {

				// Return a filtered array
				return this.categories.filter(categorie => {
					
					// Set filter by check every word of search text
					return this.searchTerm
							.toLowerCase()
							.split(' ')
							.every(word => {
								return 	categorie.categoryName.toLowerCase().includes(word)
										
							});
				});
       

			}
		else {
				return this.categorie
			}
		},
  }

}
</script>

<style>

</style>-->