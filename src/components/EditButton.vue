<template>
  <button class="edit-button" @click="onEdit">
    Save
  </button>
</template>
<script>
  import axios from 'axios';

  export default {
    props: {
      employeeData: {
        type: Object,
        required: true,
        default: {}
      }
    },
    methods: {
      onEdit(){
        let id = this.employeeData.id
        axios.put(`https://jsonplaceholder.typicode.com/posts/${id}`, this.employeeData)
          .then(response => {
            console.log(response);
            this.$emit('cancelEditMod');
          })
          .catch(err => {
            console.log(err);
          });
      }
    }
  };
</script>
<style lang="scss" scoped>
  .edit-button{
    
  }
</style>