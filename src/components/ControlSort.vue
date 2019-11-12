<template>
  <div class="col-12">
    <div class="form-group">
      <b-dropdown text="Sort by">
        <b-dropdown-item v-on:click="handleSort('name', 'asc')">Name ASC</b-dropdown-item>
        <b-dropdown-item v-on:click="handleSort('name', 'desc')">Name DESC</b-dropdown-item>
        <b-dropdown-divider></b-dropdown-divider>
        <b-dropdown-item v-on:click="handleSort('level', 'asc')">Level ASC</b-dropdown-item>
        <b-dropdown-item v-on:click="handleSort('level', 'desc')">Level DESC</b-dropdown-item>
      </b-dropdown>
      <span class="order badge badge-success badge-medium">{{orderBy}} - {{orderDir}}</span>
    </div>
  </div>
</template>

<script>
export default {
  name: 'control-sort',
  props: {
    orderBy: { type: String, default: '' },
    orderDir: { type: String, default: '' }
  },

  data() {
    return {

    }
  },
  methods: {
    handleSort(oderBy, oderDir) {
      console.log(oderBy, ' - ', oderDir)
    }
  }
}
</script>

<style>
  .order {
    text-transform: uppercase;
  }
</style>
