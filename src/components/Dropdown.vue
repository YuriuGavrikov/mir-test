<script setup>
import { ref } from "vue";
import ModalDeleteTask from "./ModalDeleteTask.vue";

defineProps({
	task: Object,
	deleteTask: Function,

	setIsEdit: Function,
});

const isModalDeleteTask = ref(false);
const setIsModalDeleteTask = () => {
	isModalDeleteTask.value = !isModalDeleteTask.value;
};
</script>

<template>
	<div class="dropdown">
		<button class="dropbtn">
			<div class="circle"></div>
			<div class="circle"></div>
			<div class="circle"></div>
		</button>

		<div class="dropdown-content">
			<a class="edit" @click="setIsEdit()" href="#">Редактировать</a>
			<a class="delete" @click="setIsModalDeleteTask()" href="#">Удалить</a>
		</div>
		<ModalDeleteTask
			v-if="isModalDeleteTask"
			:setIsModalDeleteTask="setIsModalDeleteTask"
			:deleteTask="deleteTask"
			:task="task"
		/>
	</div>
</template>

<style scoped>
.dropbtn {
	display: flex;
	align-items: center;
	gap: 1px;

	height: 1rem;
	width: 1rem;
	border: none;
	background-color: inherit;
}

.circle {
	border: 2.5px solid #86949e;
	border-radius: 50%;
	height: 0.3em;
	width: 0.3em;
}

.dropdown {
	position: absolute;
	right: 7px;
	top: 10px;
}
.dropdown-content {
	display: none;
	position: absolute;
	left: -160px;
	width: 180px;
	padding: 10px 0;
	border-radius: 4px;
	background-color: white;
	box-shadow: 0px 8px 16px 0px rgba(0, 0, 0, 0.2);
	z-index: 10;
}
.dropdown-content a {
	color: black;
	padding: 6px 10px;
	text-decoration: none;
	display: block;
}

.dropdown-content a:hover {
	background-color: #e1f1ff;
}

.dropdown:hover .dropdown-content {
	display: block;
}

.dropdown:hover .circle {
	border: 2.5px solid #3d86f4;
}

.edit::before {
	position: relative;
	content: url(../assets/edit.png);
	top: 4px;
	line-height: 0;
	margin-right: 10px;
}

.delete::before {
	position: relative;
	content: url(../assets/del.png);
	top: 4px;
	line-height: 0;
	margin-right: 10px;
}
</style>
