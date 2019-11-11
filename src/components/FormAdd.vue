<template>
  <div class="form-group add-task">
    <button 
      v-if="!isShowForm"
      v-on:click="onClickAddTask"
      type="button" class="btn btn-info btn-block">Add Task</button>
    <button 
      v-else
      v-on:click="onClickAddTask"
      type="button" class="btn btn-primary btn-block">Close Form</button>
  </div>
</template>

<script>
export default {
  name: 'form-add',
  props: {
    isShowForm: { type: Boolean, default: false }
  },
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
