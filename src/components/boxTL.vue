<template>
  <div class="container p-3 my-3 border">

    <!-- Title-->
    <h3>{{ categoryName }}</h3>
    <!--New Task Input-->
   
    <div class="d-d-flex justify-content-center">
       <input type="text"  placeholder="Add a Task"  :value="modelValue" @input="(event) => $emit('update:modelValue', event.target.value)" @keyup.enter="submitTask(id)"/>
      <button class="btn btn-dark" @click="submitTask(id)">SUBMIT</button>
      <br />
    </div>
     <!-- <button class="btn btn-dark" @click="deleteChecklist">Delete Checklist</button> -->

    <!-- List Tasks-->
    <table class="table table-bordered mt-5">
      <thead>
        <tr>
          <th scope="col">Status</th>
          <th scope="col">Task</th>
          <th scope="col">Edit</th>
          <th scope="col">Delete</th>
        </tr>
      </thead>
      <tbody v-for="task in tasks"  :key="task.id " >
        <tr  v-if="task.categoryId == id">

          <td>
             <input class="form-check-input" type="checkbox" value="" id="flexCheckDefault" @click="taskStatus(this.id)" v-model="task.status">
          </td>
          <td >
            <h5 :class="{isChecked:task.status }" > {{ task.taskName }}</h5>
          </td>
  
  
          <td>
            <div class="text-center">
             <button ><i class="bi bi-pencil-fill" ></i></button>  <!--Darkmode : <i class="bi bi-pencil"></i>-->

            </div>
          </td>
          
          <td>
            <div class="text-center">
             <button v-on:click="removeTask(id)"><i class="bi bi-trash-fill"></i></button>  <!--Darkmode : <i class="bi bi-trash"></i>-->
            </div>
          </td>
         
        </tr>
      </tbody>
    </table>
  </div>
  
  

  
</template>
<script>
export default {
  props: {
    id: {
      type: Number,
      required: false,
    },
    categoryName: {
      type: String,
      required: false,
    },
    tasks: {
      type: Array
      },
    newTask: {
     type: String ,
     default: ""
    },
     'modelValue': String,
  },
  
  methods: {
  
    submitTask() {
     console.log(this.newTask);
     this.$emit("submitTask",this.id );
      
      },

    removeTask() {
    
     this.$emit("removeTask",this.id );
      
      },
    taskStatus() {
    
     this.$emit("taskStatus",this.id );
      
      },
     deleteChecklist() {
     this.$emit("deleteChecklist",this.id );
     }
     
  },
  
};
</script>
<style scoped>


</style> 
