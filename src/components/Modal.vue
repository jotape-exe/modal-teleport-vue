<template>
    <teleport to="#modal-container">
        <transition name="modal-fade">
            <div class="bg-modal" v-if="open">
                <div class="card-modal" :style="{ height, width }">
                    <div class="modal-header">
                        <h2>{{ title }}</h2>
                        <CloseIcon class="close-icon" @click="open = false" />
                    </div>
                    <div :style="{ maxHeight: getMaxheightModal }" class="modal-content">
                        <slot></slot>
                    </div>
                </div>
            </div>
        </transition>
    </teleport>
</template>
<script setup>
import CloseIcon from './icons/CloseIcon.vue';
import { defineModel, computed } from 'vue';

const { height } = defineProps({
    width: {
        type: String,
        default: '400px',
    },
    height: {
        type: String,
        default: 'auto',
    },
    title: {
        type: String,
        default: 'Titulo do Modal',
    },
});

const open = defineModel();

const getMaxheightModal = computed(() => `calc(${height} - 20%)`)
</script>

<style scoped>
.modal-fade-enter-active,
.modal-fade-leave-active {
    transition: opacity 0.3s ease, transform 0.3s ease;
}

.modal-fade-enter-from,
.modal-fade-leave-to {
    opacity: 0;
}

.modal-fade-leave-from {
    opacity: 1;
    transform: scale(1);
}

.close-icon {
    border-radius: 10px;

    &:hover {
        cursor: pointer;
        background-color: rgba(0, 0, 0, 0.178);
    }
}

.modal-content {
    overflow-y: auto;
    scrollbar-width: thin;
}

.modal-header {
    width: 100%;
    display: flex;
    justify-content: space-between;
    align-items: start;

    h2 {
        font-weight: 600;
    }
}

.bg-modal {
    position: fixed;
    top: 0;
    left: 0;
    z-index: 9999;
    height: 100vh;
    width: 100vw;
    background-color: rgba(0, 0, 0, 0.5);
    display: flex;
    align-items: center;
    justify-content: center;
}

.card-modal {
    position: relative;
    background-color: rgb(63, 63, 63);
    border-radius: 10px;
    padding: 20px;
    margin: 0 auto;
    overflow-y: hidden;
}
</style>