<script setup>
const props = defineProps({
    level: Number
})
const emit = defineEmits(['select-mode'])
</script>

<template>
    <div class="item" @click="emit('select-mode', level)">
        <span class="label">{{ props.level }}x{{ props.level }}</span>
    </div>
</template>

<style scoped lang="scss">
.item {
    display: flex;
    justify-content: center;
    align-items: center;
    border: 2px solid #EE9d9d;
    border-radius: 20px;
    width: 150px;
    height: 150px;
    position: relative;
    margin: 0 3em;
    cursor: pointer;

    & .label {
        color: white;
        font-size: 18pt;
    }

    &:hover {
        background-color: #EE9d9d;
    }
}
</style>