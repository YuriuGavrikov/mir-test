<script setup>
import { ref } from "vue";
import Task from "./Task.vue";
import Textarea from "./Textarea.vue";

defineProps({
	title: String,
	color: String,

	tasks: Array,
	addtask: Function,
	deleteTask: Function,
	editTask: Function,

	chapter: Object,
	onDragStart: Function,
});

const isWriteTask = ref(true);
const setWriteTask = () => {
	isWriteTask.value = true;
};
</script>

<template>
	<div class="chapter">
		<div class="title">{{ title }}</div>
		<div class="items">
			<Task
				v-for="task in tasks.filter((task) => task.chapterId === chapter.id)"
				@dragstart="onDragStart($event, task)"
				draggable="true"
				:task="task"
				:addtask="addtask"
				:deleteTask="deleteTask"
				:editTask="editTask"
				:chapter="chapter"
				:setWriteTask="setWriteTask"
			/>

			<button v-if="isWriteTask" @click="isWriteTask = false" class="addBtn">
				Добавить
			</button>
			<Textarea
				v-else
				:addtask="addtask"
				:chapter="chapter"
				:setWriteTask="setWriteTask"
			/>
		</div>
	</div>
</template>

<style scoped>
.chapter {
	height: 100%;
	width: 100%;
	border: 1px solid #e3e5e8;
	border-radius: 8px;
	margin: 10px;
	background-color: #f7f7f7;
	overflow: hidden;
}
.title {
	height: 2.4rem;
	font-size: 0.8rem;
	font-weight: 600;
	text-align: center;
	padding: 0.7rem;
	background-color: v-bind(color);
}
.items {
	height: calc(100% - 2.4rem);
	display: flex;
	flex-direction: column;
	gap: 5px;
	padding: 8px 8px 8px 8px;
	overflow-y: scroll;
	overflow-x: hidden;
}
.items::-webkit-scrollbar {
	width: 10px;
}

.items::-webkit-scrollbar-thumb {
	background-color: #c4cad4;
	border-radius: 10px;
	border: 3px solid #f7f7f7;
}
.addBtn {
	background-color: inherit;
	border: none;
	color: #3d86f4;
	cursor: pointer;
	text-align: left;
	padding-top: 10px;
}
.addBtn::before {
	position: relative;
	content: "+";
	font-size: 30px;
	font-weight: 300;
	top: 4px;
	line-height: 0;
}
</style>
