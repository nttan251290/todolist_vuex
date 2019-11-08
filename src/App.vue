<template>
	<div id="app">
    <b-container>

      <!-- TITLE : START -->
      <comp-title />
      <!-- TITLE : END -->

      <b-row>
        <!-- CONTROL (SEARCH + SORT + ADD) : START -->
        <comp-control />
        <!-- CONTROL (SEARCH + SORT + ADD) : END -->

        <!-- FORM : START -->
        <comp-form />
        <!-- FORM : END -->
      </b-row>

      <!-- LIST : START -->
      <todo-list-table v-bind:listTask="listTask"/>
      <!-- LIST : END -->
    </b-container>
	</div>
</template>

<script>

import CompTitle from './components/CompTitle'
import CompControl from './components/CompControl'
import TodoListTable from './components/TodoListTable'
import CompForm from './components/CompForm'

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
      listTask: [
        {
          id: 1,
          taskName: '	Lorem ipsum dolor sit amet, consectetur adipisicing elit. Reiciendis ea c 1',
          level: 0 // Small
        },
        {
          id: 2,
          taskName: '	Lorem ipsum dolor sit amet, consectetur adipisicing elit. Reiciendis ea c 2',
          level: 1 // Medium
        },
        {
          id: 3,
          taskName: '	Lorem ipsum dolor sit amet, consectetur adipisicing elit. Reiciendis ea c 3',
          level: 2 // Height
        },
        {
          id: 4,
          taskName: '	Lorem ipsum dolor sit amet, consectetur adipisicing elit. Reiciendis ea c 4',
          level: 0 // Small
        }
      ]
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
