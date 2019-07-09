<template>
  <button class="edit-button" @click="onEdit">
    Save
  </button>
</template>
<script>
  export default {
    props: ['employeeData'],
    methods: {
      onEdit(){
        console.log(this.employeeData)
      }
    }
  };
</script>
<style lang="scss" scoped>
  .edit-button{
   
  }
</style>