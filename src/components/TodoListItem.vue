<template>
	<div id="todoContainer">
		<h2 :class="{ complete: item.isComplete }">{{ item.name }}</h2>
		<div id="buttonContainer">
			<button
				v-if="!item.isComplete"
				class="completeButton"
				@click="handleCompleteClick"
			>
				Mark Complete
			</button>
			<button v-else class="completeButton" @click="handleCompleteClick">
				Mark Incomplete
			</button>
			<button class="cancelButton" @click="handleDeleteClick">
				Delete Item
			</button>
		</div>
	</div>
</template>

<script>
export default {
	name: 'TodoListItem',
	props: { item: { name: String, isComplete: Boolean, id: Number } },
	setup(props, { emit }) {
		const handleCompleteClick = () => {
			emit('toggleComplete', props.item);
		};

		const handleDeleteClick = () => {
			emit('delete', props.item.id);
		};

		return { handleCompleteClick, handleDeleteClick };
	},
};
</script>

<style scoped>
#todoContainer {
	background: white;
	border-radius: 5px;
	max-width: 800px;
	height: 80px;
	width: 90%;
	margin: auto;
	margin-top: 4px;
	color: black;
	padding: 10px;
}

h2 {
	text-align: left;
	margin-top: 0;
	overflow: hidden;
	text-overflow: ellipsis;
	font-size: 20px;
}

.complete {
	text-decoration: line-through;
}

#buttonContainer {
	display: flex;
	justify-content: space-between;
	width: 250px;
}

button {
	height: 30px;
	width: 120px;
	cursor: pointer;
	border: none;
	color: white;
}

.completeButton {
	background: green;
}

.completeButton:hover {
	background: darkgreen;
}

.cancelButton {
	background: red;
}

.cancelButton:hover {
	background: darkred;
}
</style>
