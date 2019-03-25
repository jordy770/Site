<template>
    <div>
        <div v-bind:key="game.id" v-for="game in games">
            <GameItem v-bind:game="game" v-on:del-game="$emit('del-game', game._id)" />
            
        </div>
    </div>
</template>

<script>
import GameItem from './GameItem.vue';

export default {
    name: "Games",
    components: {
        GameItem
    },
    props: ["games"]
}
</script>

<style scoped>

</style>

