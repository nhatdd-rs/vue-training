<script setup>
const emit = defineEmits(['return-home'])
</script>
<template>
    <h1>Congratulations</h1>
    <h3>You have finished the game</h3>
    <a href="#" @click="emit('return-home')" class="btn btn-primary">Back</a>
</template>

<style scoped lang="scss">
h1,
h3 {
    color: white;
}

h1 {
    font-size: 28pt;
}

a {
    color: yellow;
    font-size: 18pt;
    text-decoration: none;

    &:hover {
        text-decoration: none;
    }
}
</style>