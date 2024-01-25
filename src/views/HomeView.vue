<script setup>
import { ref } from 'vue';
import CardList from '@/components/CardList.vue';
import SelectMode from '@/components/SelectMode.vue';
import GameFinished from '@/components/GameFinished.vue';

const isFinished = ref(false)
const selectedLevel = ref(0)
const cardList = ref([])

const shuffle = (arr) => {
  return arr.map((a) => ({ sort: Math.random(), value: a }))
    .sort((a, b) => a.sort - b.sort)
    .map((a) => a.value);
};

const selectedMode = (level) => {
  selectedLevel.value = level

  while (cardList.value.length < (level * level / 2)) {
    var r = Math.floor(Math.random() * 64) + 1;
    if (cardList.value.indexOf(r) === -1) {
      cardList.value.push(r);
    }
  }

  cardList.value.push(...cardList.value)
  cardList.value = shuffle(cardList.value)
}

const onFinishGame = () => {
  isFinished.value = true
}

const reset = () => {
  selectedLevel.value = 0
  isFinished.value = false
}
</script>

<template>
  <main>
    <SelectMode v-if="!selectedLevel" @selected-mode="selectedMode" />
    <CardList v-if="!isFinished && selectedLevel" @finish-game="onFinishGame" @return-home="reset" :cardList="cardList"
      :level="selectedLevel" />
    <GameFinished v-if="isFinished" @return-home="reset" />
  </main>
</template>

<style scoped lang="scss">
main {
  text-align: center;
}
</style>