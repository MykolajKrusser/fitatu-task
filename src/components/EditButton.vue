<template>
  <button class="edit-button" @click="onEdit">
    Save
  </button>
</template>
<script>
    export default {
        props: {
            onEdit: {
                type: Function,
                default: () => {
                  console.log('edited!')
                },
            },
        }
    };
</script>
<style lang="scss" scoped>
  .edit-button{
   
  }
</style>