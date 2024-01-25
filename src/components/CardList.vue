<script setup>
import { ref } from 'vue';
import CardSingle from './CardSingle.vue';

const props = defineProps({
    cardList: Array,
    level: Number
})

const emit = defineEmits(['return-home', 'finish-game'])

const isFlipped = ref([])
const isFlipping = ref([])

const flipCard = (id) => {
    if (isFlipping.value.length >= 2 || isFlipping.value.indexOf(id) >= 0) {
        return;
    }

    isFlipping.value.push(id)

    compareCards()
}

const compareCards = () => {
    if (isFlipping.value.length === 2) {
        const firstCard = isFlipping.value[0].split('-')[1]
        const secondCard = isFlipping.value[1].split('-')[1]

        if (firstCard == secondCard) {
            isFlipped.value.push(isFlipping.value[0])
            isFlipped.value.push(isFlipping.value[1])

            if (isFlipped.value.length === props.cardList.length) {
                emit('finish-game')
            }
        }

        setTimeout(resetCards, 500)
    }
}

const resetCards = () => {
    isFlipping.value = [];
}

const checkCardState = (index, cardIndex, card) => {
    return isFlipping.value.indexOf(`${(index - 1) * props.level + cardIndex}-${card}`) >= 0
        || isFlipped.value.indexOf(`${(index - 1) * props.level + cardIndex}-${card}`) >= 0
}

const getCardsInRow = (index) => {
    return props.cardList.slice((index - 1) * props.level, ((index - 1) * props.level) + props.level)
}

const getCardId = (index, cardIndex, card) => {
    return `${(index - 1) * props.level + cardIndex}-${card}`
}
</script>

<template>
    <div class="heading">
        <a href="#" @click="emit('return-home')" class="btn btn-primary">Back</a>
    </div>
    <div :class="`card-list level-${props.level}`">
        <div class="row" v-for="index in props.level" :key="index">
            <CardSingle @flip-card="flipCard" :is-flipped="checkCardState(index, cardIndex, card)"
                v-for="(card, cardIndex) in getCardsInRow(index)" :id="getCardId(index, cardIndex, card)"
                :key="cardIndex + index" :level="level" />
        </div>
    </div>
</template>

<style scoped lang="scss">
.heading {
    margin-bottom: 1em;

    & h1 {
        color: white;
        font-size: 28pt;
    }

    & a {
        color: yellow;
        font-size: 18pt;
        text-decoration: none;

        &:hover {
            text-decoration: none;
        }
    }
}

.card-list {
    margin: auto;

    &.level-4 {
        width: 450px;
    }

    &.level-6 {
        width: 650px;
    }

    &.level-8 {
        width: 850px;
    }

    &.level-10 {
        width: 1100px;
    }
}
</style>