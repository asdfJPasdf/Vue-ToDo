<template>
</template> 
<script>
export default {
    props: {
        taskIsChecked:{
            type: Boolean,
            required: true,
            default: false

         },
         taskDescription:{
             type: String, 
             required: true
         },
         deadline:{
             type: Date,
             required: false,
             default: getCurrentDate()
         }
         
        
    },
    methods:{
      getCurrentDate() {
      const current = new Date();
      const currentDate = current.getFullYear()+'-'+(current.getMonth()+1)+'-'+current.getDate();
      return currentDate;
    }
    }s
}
</script>

