<template>
  <div class="form-group add-task">
    <button
      v-on:click="onClickAddTask"
      type="button" class="btn btn-info btn-block">Add Task</button>
  </div>
</template>

<script>
export default {
  name: 'form-add',
  data() {
    return {
      
    }
  },
  methods: {
    onClickAddTask() {
      console.log('FormAdd.Vue : button Add Task click ');
      this.$emit('handleAddTask');
    }
  }
}
</script>

<style>

</style>
