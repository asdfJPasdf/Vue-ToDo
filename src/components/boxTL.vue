<template>
  <div class="container p-3 my-3 border">
    <!-- Title-->
    <h3>{{ categoryName }}</h3>
    <!--New Task Input-->
   
    <div class="d-flex">
       <input type="text"  placeholder="Add a Task"  :value="modelValue" @input="(event) => $emit('update:modelValue', event.target.value)" @keyup.enter="submitTask(id)"/>
      <button class="btn rounded-0" @click="submitTask(id)">SUBMIT</button>
      <br />
    </div>


    <!-- List Tasks-->
    <table class="table table-bordered mt-5">
      <thead>
        <tr>
          <th scope="col">Task</th>
          <th scope="col">#</th>
          <th scope="col">#</th>
        </tr>
      </thead>
      <tbody>
       
        
        <tr>
          <div v-for="task in tasks" :key="task.id " >
            <div v-if="task.categoryId == id" >
          <td>
            {{ task.taskName }}
          </td>
          </div> 
          </div> 
          <td>
          
            <div class="text-center">
              <span class="fa fa-pen"></span>pen
            </div>
            
          </td>
          
          <td>
            <div class="text-center">
              <span class="fa fa-trash"></span>trash
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
    // console.log(this.newTask);
     this.$emit("submitTask",this.id );
      
      },

  },
  




};
</script>