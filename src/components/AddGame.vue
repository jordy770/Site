<template>
    <div>
        <form @submit="addGame">
            <h3 class="text">Create game</h3>
            <input type="text" v-model="title" name="title" placeholder="Title">
            <input type="text" v-model="studio" name="studio" placeholder="Producer">
            <input type="text" v-model="genre" name="genre" placeholder="Genre">
            <input type="submit" value="Add Game" class="btn">
        </form>
    </div>
</template>

<script>
// import uuid from 'uuid';
export default {
    name: "AddGame",
    data() {
        return {
            title:'',
            studio:'',
            genre:''
        }
    },
    methods: {
        addGame(e) {
            e.preventDefault();
            const newGame = {
                title: this.title,
                studio: this.studio,
                genre: this.genre
            }
            // send up to parent
            this.$emit('add-game', newGame);
            this.title = "",
            this.studio = "",
            this.genre = "";
        }
    }
}
</script>

<style scoped>
    form {
        width: 20%;
        margin: 20px;
        float: left;
    }

    input[type="text"] {
        width: 100%;
        display: block;
        padding: 10px;
    }

    input[type="submit"] {
        width: 100%;
    }

    .text{
        text-align: center;
    }
</style>

