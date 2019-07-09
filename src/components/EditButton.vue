<template>
  <button class="edit-button" @click="onEdit">
    Save
  </button>
</template>
<script>
  import axios from 'axios';

  export default {
    props: {
      employeeData: Object
    },
    methods: {
      onEdit(){
        axios.post('https://jsonplaceholder.typicode.com/posts', this.employeeData)
          .then(response => {
              console.log(response);
              this.$emit('cancelEditMod')
          })
          .catch(err => {
            console.log(err)
          })
      }
    }
  };
</script>
<style lang="scss" scoped>
  .edit-button{
   
  }
</style>