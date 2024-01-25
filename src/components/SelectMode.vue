<script setup>
import ModeItem from './ModeItem.vue';

const emit = defineEmits(['selected-mode']);

const selectMode = (level) => {
    emit('selected-mode', level)
}
</script>

<template>
    <div class="main">
        <div class="title">
            Select Level
        </div>
        <div class="mode-list">
            <ModeItem @select-mode="selectMode" :level="4"></ModeItem>
            <ModeItem @select-mode="selectMode" :level="6"></ModeItem>
            <ModeItem @select-mode="selectMode" :level="8"></ModeItem>
            <ModeItem @select-mode="selectMode" :level="10"></ModeItem>
        </div>
    </div>
</template>

<style scoped>
.main {
    width: 100%;
    height: 100%;
    text-align: center;

    & .title {
        font-size: 30pt;
        color: white;
        margin-bottom: 2em;
    }

    & .mode-list {
        display: flex;
        justify-content: center;
        align-items: center;
    }
}
</style>