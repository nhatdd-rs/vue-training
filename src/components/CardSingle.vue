<script setup>
import { ref } from 'vue';

const emit = defineEmits(['flip-card'])

const props = defineProps({
    id: String,
    level: Number,
    isFlipped: Boolean
})

const imageUrl = ref(`/images/${props.id.split('-')[1]}.png`)
const backImageUrl = ref(`/images/icon_back.png`)
</script>

<template>
    <div :class="`single columns-${level}`">
        <div :class="`container ${props.isFlipped ? 'flipped' : ''}`" @click="emit('flip-card', props.id)">
            <div v-if="props.isFlipped" class="front" :id="props.id">
                <img :src="imageUrl" />
            </div>
            <div v-else class="back">
                <img :src="backImageUrl" />
            </div>
        </div>
    </div>
</template>

<style scoped lang="scss">
.single {
    display: inline-block;
    justify-content: center;
    align-items: center;
    margin: 10px;

    &.columns-4 {
        width: calc(100% / 4 - 20px);
    }

    &.columns-6 {
        width: calc(100% / 6 - 20px);
    }

    &.columns-8 {
        width: calc(100% / 8 - 20px);
    }

    &.columns-10 {
        width: calc(100% / 10 - 20px);
    }

    & .container {
        text-align: center;
        display: flex;
        max-width: 100px;
        justify-content: center;
        align-items: center;
        border: 2px solid #EE9d9d;
        border-radius: 20px;
        background-color: #EE9d9d;

        & img {
            max-width: 100%;
            max-height: 70px;
        }

        &.flipped {
            background-color: transparent;
        }
    }
}
</style>