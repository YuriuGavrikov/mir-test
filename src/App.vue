<script setup>
import { ref, watch, onMounted } from "vue";

import Chapter from "./components/Chapter.vue";
// import Alert from "./components/Alert.vue";

const tasks = ref([
	{ id: 0, text: "task1", chapterId: 0 },
	{ id: 1, text: "task2", chapterId: 0 },
	{ id: 2, text: "task3", chapterId: 0 },
	{ id: 3, text: "task4", chapterId: 0 },
]);

const addtask = (text, chapterId) => {
	tasks.value.push({
		id: Date.now(),
		text: text,
		chapterId: chapterId,
	});

	alert(
		`Задача создана в "${
			chapters.value.find((item) => item.id === chapterId).title
		}" "${text.value}"`
	);
};

const deleteTask = (task) => {
	tasks.value.splice(
		tasks.value.findIndex((n) => n.id === task.id),
		1
	);
	alert(`Задача удалена "${task.text}"`);
};

const editTask = (task, editText) => {
	tasks.value[tasks.value.findIndex((n) => n.id === task.id)].text = editText;
};

onMounted(() => {
	tasks.value = localStorage.getItem("tasks")
		? JSON.parse(localStorage.getItem("tasks"))
		: tasks.value;
});

watch(
	tasks,
	async (newTasks, oldTasks) => {
		localStorage.setItem("tasks", JSON.stringify(newTasks));
	},
	{ deep: true }
);

const chapters = ref([
	{ id: 0, title: "На согласовании", color: "#FF65DD" },
	{ id: 1, title: "Новые", color: "#33A0FF" },
	{ id: 2, title: "В процессе", color: "#FFC633" },
	{ id: 3, title: "Готово", color: "#22C33D" },
	{ id: 4, title: "Доработать", color: "#F53D5C" },
]);

const onDragStart = (e, task) => {
	e.dataTransfer.dropEffect = "move";
	e.dataTransfer.effectAllowed = "move";
	e.dataTransfer.setData("taskId", task.id.toString());
};

const onDrop = (e, chapterId) => {
	const taskId = parseInt(e.dataTransfer.getData("taskId"));
	let usedTask = {};
	tasks.value = tasks.value.map((task) => {
		if (task.id === taskId) {
			task.chapterId = chapterId;
			usedTask = task;
		}
		return task;
	});
	alert(
		`Задача перенесена в "${
			chapters.value.find((item) => item.id === chapterId).title
		}" "${usedTask.text}"`
	);
};
</script>

<template>
	<!-- <Alert /> -->
	<div class="container">
		<Chapter
			v-for="chapter in chapters"
			@drop="onDrop($event, chapter.id)"
			@dragover.prevent
			@dragenter.prevent
			:key="chapter.id"
			:tasks="tasks"
			:addtask="addtask"
			:deleteTask="deleteTask"
			:editTask="editTask"
			:chapter="chapter"
			:onDragStart="onDragStart"
			:title="chapter.title"
			:color="chapter.color"
		/>
	</div>
</template>

<style scoped>
.container {
	display: flex;
	justify-content: space-between;

	height: 100vh;
	min-width: 1280px;
	padding: 48px 52px;
}
</style>
