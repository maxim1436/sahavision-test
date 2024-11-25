<template>
    <li>
        <span @click.stop="toggle" :class="{ selected: isSelected }">{{ isOpen ? '▼' : '▶' }} {{ folder.name }}</span>
        <ul v-if="isOpen">
            <FolderNode v-for="child in folder.children" :key="child.id" :folder="child" :selectedId="selectedId"
                @select="$emit('select', $event)" />
        </ul>
    </li>
</template>

<script setup lang="ts">
import { PropType, ref, computed } from 'vue';
import { Folder } from '@/types';

const props = defineProps({
    folder: {
        type: Object as PropType<Folder>,
        required: true
    },
    selectedId: {
        type: Number as PropType<number | null>,
        default: null
    }
});
const isOpen = ref(false);
const isSelected = computed(() => props.folder.id === props.selectedId);

const emit = defineEmits<{
    (e: 'select', value: number): void,
}>();

const toggle = () => {
    emit('select', props.folder.id);
    isOpen.value = !isOpen.value;
};

</script>

<style scoped>
ul {
    list-style-type: none;
    padding-left: 20px;
    margin: 5px 0;
}

li {
    margin: 5px 0;
}

span {
    cursor: pointer;
    color: #007bff;
    transition: color 0.3s;
}

span:hover {
    color: #0056b3;
}

.selected {
    font-weight: bold;
    color: #28a745;
    background-color: rgba(40, 167, 69, 0.1);
    border-left: 4px solid #28a745;
    padding-left: 8px;
}
</style>