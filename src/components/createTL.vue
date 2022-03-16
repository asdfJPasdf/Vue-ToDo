<template>
  
    <div class= "d-flex">
        <input type="text" placeholder="Add Task List" class="form-control-sm" v-model="newCategory">
        <button button class="btn  rounded-0" @click="createChecklist">create Checklist</button> 
        <br>
    </div> 
</template>


<script>
export default{
    props: {
        categories:[{
            id:{
            type: Number,
            required: false
        },
        categoryName: {
            type: String,
            required: false 
        },
        tasks: [{
            id: {type: Number,required: false },
            name: {type: String,required: false },
            status: {type: Boolean,default: false},
        }],
        
        newCategory:{
            type: String,
            default: ""
        },
        
    }],
    methods: {
    createChecklist(){
                if(this.newCategory.lenght === 0) return;
                this.categories.push({
                    id: this.categories.lenght++, 
                    categoryName: this.newCategory,
                    tasks: []
            });
            
    }
    }
}}
</script>