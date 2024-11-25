<template>
    <div class="modal" v-show="isVisible">
        <div class="modal-content">
            <header>
                <h2>{{ title }}</h2>
                <button @click="$emit('close')">✖</button>
            </header>
            <div class="folder-tree-container">
                <FolderTree :folders="folders" :selectedId="selectedId" @select="handleSelect" />
            </div>
            <footer>
                <button @click="confirmSelection">Ок</button>
                <button @click="$emit('close')">Закрыть</button>
            </footer>
        </div>
    </div>
</template>

<script setup lang="ts">
import { Folder } from '@/types';
import { PropType, ref } from 'vue';
import FolderTree from './FolderTree.vue';

defineProps({
    isVisible: {
        type: Boolean,
        required: true
    },
    title: {
        type: String,
        required: true
    },
    folders: {
        type: Array as PropType<Folder[]>,
        required: true
    }
});

const selectedId = ref<number | null>(null);

const handleSelect = (id: number) => {
    selectedId.value = id;
};

const emit = defineEmits<{
    (e: 'select', value: number): void,
    (e: 'close'): void,
}>();

const confirmSelection = () => {
    if (selectedId.value !== null) {
        emit('select', selectedId.value);
        selectedId.value = null;
    }
};

</script>

<style scoped>
.modal {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background-color: rgba(0, 0, 0, 0.7);
    display: flex;
    justify-content: center;
    align-items: center;
    z-index: 1000;
}

.modal-content {
    background-color: #fff;
    border-radius: 12px;
    padding: 30px;
    box-shadow: 0 4px 20px rgba(0, 0, 0, 0.15);
    width: 400px;
    animation: appear 0.3s ease;
}

@keyframes appear {
    from {
        opacity: 0;
        transform: translateY(-20px);
    }

    to {
        opacity: 1;
        transform: translateY(0);
    }
}

header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 20px;
}

h2 {
    margin: 0;
    font-size: 18px;
    color: #333;
}

button {
    background: none;
    border: none;
    cursor: pointer;
    font-size: 24px;
    color: #888;
    transition: color 0.3s;
}

button:hover {
    color: #ff4c4c;
}

footer {
    display: flex;
    justify-content: space-between;
    margin-top: 20px;
}

footer button {
    padding: 10px 16px;
    background-color: #007bff;
    color: #fff;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    transition: background-color 0.3s;
}

footer button:hover {
    background-color: #0056b3;
}
</style>