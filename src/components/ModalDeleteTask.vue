<script setup>
defineProps({
	task: Object,
	deleteTask: Function,
	setIsModalDeleteTask: Function,
});
</script>

<template>
	<div class="modalBg">
		<div class="modalDeleteTask">
			<div class="title">Удалить задачу?</div>
			<div class="text">{{ task.text }}</div>
			<div class="btns">
				<button @click="deleteTask(task), setIsModalDeleteTask()" class="btn">
					Удалить
				</button>
				<button @click="setIsModalDeleteTask()" class="btn">Отменить</button>
			</div>
			<button @click="setIsModalDeleteTask()" class="cross">×</button>
		</div>
	</div>
</template>

<style scoped>
.modalBg {
	display: block;
	background: rgba(0, 0, 0, 0.6);
	position: fixed;
	width: 100%;
	height: 100%;
	left: 0;
	right: 0;
	top: 0;
	bottom: 0;
	z-index: 20;
}
.modalDeleteTask {
	position: absolute;

	top: calc(50% - 90px);
	left: calc(50% - 250px);

	display: flex;
	flex-direction: column;
	align-items: start;
	justify-content: space-between;

	width: 500px;
	min-height: 196px;

	padding: 40px;

	background-color: white;

	border-radius: 8px;
	box-shadow: 0px 5px 15px 0px rgba(34, 60, 80, 0.2);
}
.title {
	font-size: 1.8rem;
	font-weight: 600;
}
.text {
}
.btns {
	display: flex;
	justify-content: space-between;
	gap: 10px;

	width: 100%;
}
.btn {
	width: 100%;
	padding: 8px;

	background-color: inherit;

	border: 1px solid #c4cad4;
	border-radius: 4px;
	cursor: pointer;
}
.btn:hover {
	box-shadow: 0px 5px 15px 0px rgba(34, 60, 80, 0.2);
}
.cross {
	position: absolute;
	top: 20px;
	right: 20px;

	font-size: 2rem;
	line-height: 0.7;

	border: none;
	background-color: inherit;
	color: #86949e;

	cursor: pointer;
}
</style>
