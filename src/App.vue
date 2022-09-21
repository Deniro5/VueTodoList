<template>
	<div id="app">
		<input
			id="newTodoInput"
			type="text"
			v-model="newTodo"
			placeholder="Type name of new item and press enter"
			@keyup="handleEnterListen"
		/>
		<div id="listContainer">
			<TodoListItem
				v-for="item in items"
				:key="item"
				:item="item"
				@toggleComplete="handleToggleComplete"
				@delete="handleDelete"
			/>
		</div>
	</div>
</template>

<script>
import { ref } from 'vue';
import TodoListItem from './components/TodoListItem.vue';

export default {
	name: 'App',
	components: {
		TodoListItem,
	},
	setup() {
		const newTodo = ref('');
		const items = ref([]);
		const id = ref(1);

		const handleEnterListen = (e) => {
			if (e.key === 'Enter') {
				newTodo.value = e.target.value;
				handleAddItem();
			}
		};

		const handleAddItem = () => {
			const newItem = {
				id: id.value,
				name: newTodo.value,
				isComplete: false,
			};
			items.value.push(newItem);
			id.value++;
			newTodo.value = '';
		};

		const handleToggleComplete = (item) => {
			item.isComplete = !item.isComplete;
		};

		const handleDelete = (itemId) => {
			items.value = items.value.filter((item) => item.id !== itemId);
		};

		return {
			items,
			newTodo,
			handleEnterListen,
			handleToggleComplete,
			handleDelete,
		};
	},
};
</script>

<style>
#app {
	font-family: Avenir, Helvetica, Arial, sans-serif;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	text-align: center;
	color: white;
	text-align: center;
}

body {
	background: black;
	color: white;
	margin-top: 20px;
}

#newTodoInput {
	width: 300px;
	height: 15px;
	padding: 5px;
}

#listContainer {
	margin-top: 35px;
	text-align: center;
	height: calc(100vh - 86px);
	overflow: scroll;
}
</style>
