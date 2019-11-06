<template>
	<div id="app">
		<b-container>
			<comp-title />

			<b-row>
				<comp-control 
					v-bind:orderBy="orderBy"
					v-bind:orderDir="orderDir"
					v-bind:strSearch="strSearch"
					v-on:handleSort="handleSort"
					v-on:handleSearch="handleSearch"
				/>

				<comp-form 
					v-bind:isShowForm="isShowForm"
					v-on:toggleForm="toggleForm"
				/>
			</b-row>

			<todo-list-table 
				v-bind:listTask="listTaskSort"
				v-on:handleDelete="handleDelete"
			/>
		</b-container>
	</div>
</template>

<script>
/*
App
	CompForm
		FormAdd -> click 
			-> Run onClickAddTask() 
			-> Kích hoạt Event handleAddTask 
			-> Kích hoạt tiếp toggleForm

*/
// Lưu dũ liệu -> Không cần -> Mock Data, Fake Data
import TodoListTable from './components/TodoListTable';
import CompTitle from './components/CompTitle';
import CompControl from './components/CompControl';
import CompForm from './components/CompForm';

import listTask from './mocks/tasks';

export default {
	name: 'app',
	components: {
		CompForm,
		CompTitle,
		CompControl,
		TodoListTable
	},
	data () {
		return {
			listTask: listTask,
			isShowForm: false,
			strSearch: '',
			orderBy: 'name',
			orderDir: 'asc'
		}
	},
	computed: {
		listTaskSearch() {
			const { strSearch } = this;
			
			var newItems = this.listTask.filter(item => {
				return item.name.toLowerCase().includes(strSearch.toLowerCase());
			});
			// this.listTask.forEach(function(item, index) {
			// 	let lowerName = item.name.toLowerCase();
			// 	let lowerSubString = strSearch.toLowerCase();
			// 	if(lowerName.includes(lowerSubString)) 
			// 		newItems.push(item);
				
			// });
			return newItems;
		},
		listTaskSort() {
			var listTask = [...this.listTaskSearch];
				listTask.sort(this.compareSort);
				
			return listTask;
		}
	},
	// created() {
	// 	console.log('created task = ', listTask);
	// },
	methods: {
		handleDelete(taskDelete) {
			// Cách 1
			this.listTask = this.listTask.filter(item => item.id !== taskDelete.id);

			// Cách 2
			// var idxDelete = -1;
			// for(var index = 0; index < this.listTask.length; index++) {
			// 	if(this.listTask[index].id === taskDelete.id) {
			// 		idxDelete = index;
			// 		break;
			// 	}
			// }
			// if(idxDelete !== -1) this.listTask.splice(idxDelete, 1);

			console.log("handleDelete App.vue: ", taskDelete);
		},
		compareSort(a, b) {
			var numberSort = this.orderDir === 'asc' ? -1 : 1;
			
			if(a[this.orderBy] < b[this.orderBy]) return numberSort;
			else if(a[this.orderBy] > b[this.orderBy]) return numberSort * (-1);
			return 0;
		},
		handleSort(data) {
			this.orderBy = data.orderBy;
			this.orderDir = data.orderDir;
			console.log('handleSort App.vue', data);
		},
		handleSearch(data) {
			this.strSearch = data;
			console.log('handleSearch App.vue: ', data)
		},
		toggleForm() {
			console.log('toggleForm App.vue');
			this.isShowForm = !this.isShowForm;
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
