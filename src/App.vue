<template>
	<div id="app">
    <b-container>

      <!-- TITLE : START -->
      <comp-title />
      <!-- TITLE : END -->

      <b-row>
        <!-- CONTROL (SEARCH + SORT + ADD) : START -->
        <comp-control
          v-on:handleSearch="handleSearch"
          v-bind:strSearch="strSearch"
        />
        <!-- CONTROL (SEARCH + SORT + ADD) : END -->

        <!-- FORM : START -->
        <comp-form 
          v-bind:isShowForm="isShowForm" 
          v-on:toggleForm="toggleForm"/>
        <!-- FORM : END -->
      </b-row>

      <!-- LIST : START -->
      <todo-list-table v-bind:listTask="listTaskSearch"/>
      <!-- LIST : END -->
    </b-container>
	</div>
</template>

<script>

import CompTitle from './components/CompTitle'
import CompControl from './components/CompControl'
import TodoListTable from './components/TodoListTable'
import CompForm from './components/CompForm'

import listTask from './mocks/tasks'

export default {
	name: 'app',
  components: {
    TodoListTable,
    CompTitle,
    CompControl,
    CompForm
  },

	data () {
		return {
      isShowForm: false,
      listTask,
      strSearch: ''
		}
  },
  
  computed: {
    listTaskSearch() {
      const { strSearch } = this;
      let newItems = this.listTask.filter(item => {
        return item.name.toLowerCase().includes(strSearch.toLowerCase());
      });
      return newItems;
    }
  },

  methods: {
    toggleForm() {
      console.log('App.vue: toggleForm');
      this.isShowForm = !this.isShowForm;
    },

    handleSearch(data) {
      this.strSearch = data;
      console.log('handleSearch App.vue: ', data);
    }
  }
}
</script>

<style>
  body {
    padding: 100px 0;
  }
  .table>tbody>tr>td, .table>tbody>tr>th, .table>tfoot>tr>td, .table>tfoot>tr>th, .table>thead>tr>td, .table>thead>tr>th {
    vertical-align: middle;
  }

  .container > .row {
    margin-top: 20px;
    margin-bottom: 30px;
  }

  span.badge-medium {
    padding: 11px 10px;
    margin: 0px 8px;
    font-size: 16px;
    display: inline-block;
    vertical-align: top;
  }

  @media (max-width: 992px) {
    .add-task {
        margin-top: 50px;
    }
  }
</style>
