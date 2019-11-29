<template>
	<div id="app">
    <b-container>

      <!-- TITLE : START -->
      <comp-title />
      <!-- TITLE : END -->

      <b-row>
        <!-- CONTROL (SEARCH + SORT + ADD) : START -->
        <comp-control
          v-bind:orderBy="orderBy"
          v-bind:orderDir="orderDir"
          v-on:handleSearch="handleSearch"
          v-on:handleSort="handleSort"
          v-bind:strSearch="strSearch"
        />
        <!-- CONTROL (SEARCH + SORT + ADD) : END -->

        <!-- FORM : START -->
        <comp-form 
          v-bind:isShowForm="isShowForm" 
          v-bind:taskSelected="taskSelected"
          v-on:toggleForm="toggleForm"
          v-on:handleAddNewTask="handleAddNewTask"
          v-on:handleEditTaskById="handleEditTaskById" />
        <!-- FORM : END -->
      </b-row>

      <!-- LIST : START -->
      <todo-list-table
        v-on:handleEdit="handleEdit"
        v-on:handleDelete="handleDelete"
        v-bind:listTask="listTaskSort" />
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
      strSearch: '',
      orderBy: 'level',
      orderDir: 'asc',
      taskSelected: null
		}
  },
  
  watch: {
    listTask: function(newTasks) {
      let tasksString = JSON.stringify(newTasks)
      localStorage.setItem('tasks', tasksString)
      console.log('watch listTasks : ', tasksString)
    }
  },

  computed: {
    listTaskSearch() {
      const { strSearch } = this;
      let newItems = this.listTask.filter(item => {
        return item.name.toLowerCase().includes(strSearch.toLowerCase());
      });
      return newItems;
    },

    listTaskSort() {
      let listTask = [...this.listTaskSearch];
      listTask.sort(this.compareSort);
      return listTask;
    }

  },

  created() {
    // Lấy listTask từ trong localStorage
    console.log(localStorage.getItem('tasks'))
    let tasks = localStorage.getItem('tasks')
    if (tasks !== null) {
      this.listTask = JSON.parse(tasks)
    } else {
      this.listTask = []
    }
  },

  methods: {
    handleEditTaskById(taskEdit) {
      console.log('handleEditTaskById App.vue', taskEdit);
      let index = this.listTask.findIndex(item => item.id === taskEdit.id)
      console.log('idex is : ', index, taskEdit.id)

      if(index !== -1) {
        this.listTask.splice(index, 1, taskEdit)
      }

      this.toggleForm()
    },

    handleAddNewTask(newTask) {
      console.log('handleAddNewTask App.vue', newTask);
      this.listTask.push(newTask);
    },

    handleEdit(taskEdit) {
      this.taskSelected = taskEdit
      this.isShowForm = true
      console.log('handleEdit App.vue', taskEdit);
    },

    compareSort(a, b) {
      let numberSort = this.orderDir === 'asc' ? -1 : 1;

      if(a[this.orderBy] < b[this.orderBy]) return numberSort
      else if(a[this.orderBy] > b[this.orderBy]) return numberSort * (-1)
      return 0;
    },

    toggleForm() {
      if(this.isShowForm) this.taskSelected = null
      console.log('App.vue: toggleForm');
      this.isShowForm = !this.isShowForm;
    },

    handleSearch(data) {
      this.strSearch = data;
      console.log('handleSearch App.vue: ', data);
    },

    handleSort(data) {
      this.orderBy = data.orderBy;
      this.orderDir = data.orderDir;
      console.log('handleSort App.vue', data);
    },

    handleDelete(taskDelete) {
      this.listTask = this.listTask.filter(item => item.id !== taskDelete.id);
      console.log('handleDelete App.vue', taskDelete);
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
