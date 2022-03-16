<template>
  <div class="container p-3 my-3 border">
    <!-- Menu-->
    <h3>{{ categoryName }}</h3>
 
    <!-- Add Taks to List -->
  


    <!-- List Tasks-->
    <table class="table table-bordered mt-5">
      <thead>
        <tr>
          <!--  <th scope="col">Done?</th> -->
          <th scope="col">Check</th>
          <th scope="col">Task</th>
          <th scope="col">Edit</th>
          <th scope="col">Delete</th>
        </tr>
      </thead>
      <tbody>
        
        <tr v-for="task in tasks" :key="task.id">
          <td> <input class="form-check-input" type="checkbox" value="" id="flexCheckDefault"></td>
          <!--  <td>{{task.status}}</td> -->
          <td>{{ task.name }}</td>
          <td>
            <div class="text-center"><span class="bi bi-pencil-fill"></span></div>
          </td>
          <td>
            <div class="text-center">
              <span class="bi bi-trash-fill"></span>
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
  },

  methods: {
    submitTask() {
   
    console.log(this.newTask);
    this.$emit("submitTask", this.newTask);

      },
      /*removeTask(id){
        this.$emit("remove-Task", this.id)

      },*/
    handleInput () {
    this.$emit('input', this.content)
    }
  },
  
  data: function () {

       return {
      content: this.value
    }
  },



};
</script>