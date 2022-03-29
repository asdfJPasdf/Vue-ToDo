<template>
<h1>Tasks</h1>
    <div class= "d-flex justify-content-center" style="position:absolute top:5px" >
     <input type="text" placeholder="Search.." class="form-control-sm" v-model="searchTerm" > 
     <div style=" margin-left: 80px;">
      <input type="checkbox" class="form-check-input" v-model=" onlyUnchecked" id="onlyUnchecked">
      <label for="onlyUnchecked"  style="margin-left: 10px;"> Only Show Unchecked Tasks </label>
      </div> 
        <br>
       
       
    </div> 
    <div class="container" v-if="onlyUnchecked">
    <table v-if="filtered_Tasks.length" class="table table-bordered mt-5">
			<thead>
				<tr>
          <th scope="col" >Status</th>
					<th scope="col">Task</th>
				
				
				</tr>
			</thead>
     
			<tbody v-for="task in filtered_Tasks" :key="task.id">
				<tr v-if="!task.status">
          <td> <input class="form-check-input" type="checkbox" value="" id="flexCheckDefault" @click="taskStatus(this.id)" v-model="task.status"></td>
					<td>{{ task.taskName }}</td>
					
				
				</tr>
			</tbody>
		</table>
    
    <p v-else class="mt-2">
			It doesn't exist a task with this name
		</p>
    </div>

    <div class="container" v-else>
    <table v-if="filtered_Tasks.length" class="table table-bordered mt-5">
			<thead>
				<tr>
          <th scope="col" >Status</th>
					<th scope="col">Task</th>
				
				
				</tr>
			</thead>
     
			<tbody>
				<tr v-for="task in filtered_Tasks" :key="task.id">
          <td> <input class="form-check-input" type="checkbox" value="" id="flexCheckDefault" @click="taskStatus(this.id)" v-model="task.status"></td>
					<td>{{ task.taskName }}</td>
					
				
				</tr>
			</tbody>
		</table>
    
    <p v-else class="mt-2">
			It doesn't exist a task with this name
		</p>
    </div>
</template>

<script>
import axios from "axios";
export default {
   name: "Tasks",
  components: {
    
  },
  data() {
    return {
       tasks:[],
       searchTerm: "",
       onlyUnchecked: false
      
       


    };
  },
   async created() {
   
    
    try {
      const resTasks = await axios.get(`http://localhost:3000/tasks`);
      this.tasks = resTasks.data;
    } catch (error) {
      console.log(error);
    }
  },
  
  computed: {
  filtered_Tasks() {

			if (this.searchTerm) {

				// Return a filtered array
				return this.tasks.filter(task => {
					
					// Set filter by check every word of search text
					return this.searchTerm
							.toLowerCase()
							.split(' ')
							.every(word => {
								return 	task.taskName.toLowerCase().includes(word)
                ||
                task.status.toString().includes(word)
                
										
							});
				});
       

			}
		else {
				return this.tasks
			}
		},
  }

}
</script>

<style>

</style>