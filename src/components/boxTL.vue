<template>
  <div class="container p-3 my-3 border">
    <!-- Menu-->
    <h3>{{ categoryName }}</h3>
    <div class="d-flex">
      <input type="text" placeholder="Add Task..." class="form-control-sm" v-on:keyup.enter="submitTask" v-model="newTask" @change="handleInput"/>
      <button class="btn rounded-0" @click="submitTask">SUBMIT</button>
      <br />
    </div>
    <!-- Add-->


    <!-- List Tasks-->
    <table class="table table-bordered mt-5">
      <thead>
        <tr>
          <!--  <th scope="col">Done?</th> -->
          <th scope="col">Task</th>
          <th scope="col">#</th>
          <th scope="col">#</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="task in tasks" :key="task.id">
          <!--  <td>{{task.status}}</td> -->
          <td>{{ task.name }}</td>
          <td>
            <div class="text-center"><span class="fa fa-pen"></span>pen</div>
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
  },

  methods: {
    submitTask() {
   
    console.log(this.newTask);
    this.$emit("submitTask", this.newTask);

      },
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