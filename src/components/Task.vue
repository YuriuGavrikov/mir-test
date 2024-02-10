<script setup>
import { ref } from "vue";
import Dropdown from "./Dropdown.vue";
import Textarea from "./Textarea.vue";

defineProps({
	task: Object,

	addtask: Function,
	deleteTask: Function,
	editTask: Function,

	chapter: Object,
	setWriteTask: Function,
});

const isEdit = ref(true);
const setIsEdit = () => {
	isEdit.value = !isEdit.value;
};
</script>

<template>
	<div v-if="isEdit" class="task">
		<p>{{ task.text }}</p>
		<Dropdown :deleteTask="deleteTask" :setIsEdit="setIsEdit" :task="task" />
	</div>
	<Textarea
		v-else
		:task="task"
		:editTask="editTask"
		:chapter="chapter"
		:setWriteTask="setWriteTask"
		:setIsEdit="setIsEdit"
	/>
</template>

<style scoped>
.task {
	display: flex;
	justify-content: space-between;

	position: relative;

	padding: 8px 24px 8px 8px;
	border: 1px solid #c4cad4;
	border-radius: 4px;
	background-color: white;
	cursor: pointer;
}
.task:hover {
	box-shadow: 0px 5px 15px 0px rgba(34, 60, 80, 0.2);
}
</style>
