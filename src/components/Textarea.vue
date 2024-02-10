<script setup>
import { ref } from "vue";
import { useTextareaAutosize } from "@vueuse/core";

const props = defineProps({
	task: Object,
	addtask: Function,
	editTask: Function,

	setIsEdit: Function,

	chapter: Object,
	setWriteTask: Function,
});

const { textarea, input } = useTextareaAutosize();

const qqq = ref(props.addtask ? input : props.task.text);
// const textTask = ref(input);

const AddOrEditTask = (
	task,
	addtask,
	editTask,
	chapter,
	setWriteTask,
	setIsEdit
) => {
	if (addtask) {
		input.value ? addtask(input, chapter.id) : null, setWriteTask();
	} else if (editTask) {
		qqq
			? (editTask(task, qqq), setWriteTask(), setIsEdit())
			: (null, setWriteTask(), setIsEdit());
	}
};

const vFocus = {
	mounted: (el) => el.focus(),
};
</script>

<template>
	<div class="wrapTextarea">
		<textarea
			v-focus
			ref="textarea"
			v-model="qqq"
			class="textarea"
			placeholder="Введите текст..."
		/>
		<div class="textareaBtns">
			<button
				class="deleteBtn"
				@click="
					addtask ? (setWriteTask(), (input = '')) : null;
					editTask ? (setIsEdit(), (input = '')) : null;
				"
			></button>
			<button
				class="successBtn"
				@click="
					AddOrEditTask(
						task,
						addtask,
						editTask,
						chapter,
						setWriteTask,
						setIsEdit
					)
				"
			></button>
		</div>
	</div>
</template>

<style scoped>
.wrapTextarea {
	position: relative;
}
.textarea {
	width: 100%;
	min-height: 55px;
	border: 1px solid #3d86f4;
	border-radius: 4px;
	resize: none;
	overflow: hidden;
	padding: 8px 30px 8px 8px;
	background-color: white;
	outline: none;
}

.textareaBtns {
	display: flex;
	flex-direction: column;
	position: absolute;
	top: 10px;
	right: 5px;
}
.deleteBtn {
	width: 20px;
	height: 20px;
	background-image: url(../assets/X.png);
	background-position: center;
	background-repeat: no-repeat;
	border: none;
	background-color: inherit;
}
.successBtn {
	width: 20px;
	height: 20px;
	margin-left: 1px;
	background-image: url(../assets/ok.png);
	background-position: center;
	background-repeat: no-repeat;
	border: none;
	background-color: inherit;
}
</style>
