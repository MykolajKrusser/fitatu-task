<template>
  <button class="edit-button" @click="onEdit">
      Edit
  </button>
</template>
<script>
    export default {
        props: {
            onEdit: {
                type: Function,
                default: () => {console.log('edited!')},
            },
        },
        components: {
            
        },
    };
</script>
<style lang="scss" scoped>
  .edit-button{
    background: #999d9d;
    color: black;
  }
</style>