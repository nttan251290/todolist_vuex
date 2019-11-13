<template>
  <tr>
    <td class="text-center">{{index}}</td>
    <td>{{task.name}}</td>
    <td class="text-center"><span class="badge" v-bind:class="classLevel">{{getLevelName}}</span></td>
    <td>
      <button type="button" class="btn btn-warning">Edit</button>
      <button type="button" class="btn btn-danger" v-on:click="handleDelete">Delete</button>
    </td>
  </tr>
</template>

<script>
import mapLevel from '../mocks/lelvel'

export default {
  name: 'todo-list-item',

  props: {
    task: { type: Object, default: {} },
    index: Number
  },

  computed: {
    getLevelName() {
      return this.mapLevel[this.task.level].name
    },

    classLevel() {
      return this.mapLevel[this.task.level].class
    }
  },

  data() {
    return {
      mapLevel
    }
  },

  methods: {
    handleDelete() {
      if(confirm('Do you want to delete this tak ?')) {
        console.log('handledelete TodoListItem.vue');
        this.$emit('handleDelete', this.task);
      }
    }
  }
}
</script>

<style>

</style>
