<template>
  
    
</template>


<script>
export default{
    props: {
        categories:[{
            id:{
            type: Number,
          
        },
        categoryName: {
            type: String,
        
        },
        tasks: {
            type: Array 
        },
        
        /*newCategory:{
            type: String,
            default: ""
        },*/
        
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