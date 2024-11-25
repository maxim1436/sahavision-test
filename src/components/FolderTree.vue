<template>
	<div>
		<ul>
			<FolderNode v-for="folder in folders" :key="folder.id" :folder="folder" :selectedId="selectedId"
				@select="handleSelect" />
		</ul>
	</div>
</template>

<script setup lang="ts">
import { PropType, defineProps } from 'vue';
import FolderNode from './FolderNode.vue';
import { Folder } from '@/types';

defineProps({
	folders: {
		type: Array as PropType<Folder[]>,
		required: true
	},
	selectedId: {
		type: Number as PropType<number | null>,
		default: null
	}
});

const emit = defineEmits<{
	(e: 'select', value: number): void,
}>();

const handleSelect = (id: number) => {
	emit('select', id);
}

</script>

<style scoped>
ul {
	list-style-type: none;
	padding-left: 20px;
	margin: 10px 0;
}

li {
	margin: 5px 0;
	font-size: 16px;
}

span {
	cursor: pointer;
	color: #007bff;
	transition: color 0.3s, font-weight 0.3s;
}

span:hover {
	color: #0056b3;
	font-weight: bold;
}

li::before {
	content: '';
	position: absolute;
	left: -12px;
	top: 50%;
	width: 8px;
	height: 8px;
	background: #c0c0c0;
	border-radius: 50%;
	transform: translateY(-50%);
}

.selected {
	font-weight: bold;
	color: #28a745;
	background-color: rgba(40, 167, 69, 0.1);
	border-radius: 4px;
	padding: 4px;
}
</style>