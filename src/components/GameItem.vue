<template>
    <div id="container">
        <br/>
        <div class="game-item">
            <button class="down" @click="toggle()"> Details </button>
            <b>{{game.title}}</b>
            <button class="edit" @click="toggle1()"> Edit </button>
            <button @click="$emit('del-game', game.id)" class="del"> X</button> <!-- Emit delete to parent -->
            <ul v-show="isOpen" class="list">
                <li><b>Producer:</b> {{game.studio}}</li>
                <li><b>Genre:</b> {{game.genre}}</li>
                <li><b>ID:</b> {{game._id}}</li>
            </ul>
            <form @submit="editGame" v-show="isOpen1">

                <input type="text" name="title" v-model="title">
                <input type="text" name="studio" v-model="studio">
                <input type="text" name="genre" v-model="genre">
                <input type="submit" value="Edit Game" class="btn">
            </form>
        </div>
    </div>
</template>

<script>
export default {
    name:"GameItem",
    props: ["game"],
    data() {
        return {
            isOpen: false,
            isOpen1: false,
            
            title:'',
            studio:'',
            genre:''
        }
    },
    methods: {
        toggle() {
            this.isOpen = !this.isOpen
        },
        toggle1() {
            this.isOpen1 = !this.isOpen1
        },

        editGame(e) {
            e.preventDefault();
            const editGame = {
                title: this.title,
                studio: this.studio,
                genre: this.genre
            }
            // send up to parent
            this.$emit('edit-game', editGame);
            this.title = "",
            this.studio = "",
            this.genre = "";
        }
    }
}
</script>

<style scoped>
    .game-item {
        background: #f4f4f4;
        padding-left: 20px;
        padding-right: 20px;
        padding-top: 10px;
        padding-bottom: 10px;
        border-width: 2px;
        border-style: solid;
        border-color: #1a1a1a;
        margin-left: auto;
        margin-right: auto;
        width: 50%;
    }

    .del {
        background: #ff0000;
        color: #fff;
        border: none;
        padding: 5px 9px;
        border-radius: 50%;
        cursor: pointer;
        float: right;
    }
    
    button.down {
        border: 1px solid gray;
        background: #1a1a1a;
        color: white;
        padding: 7px 13px;
        margin-right: 12px;
        margin-left: 0;
    }

    button.edit {
        border: 2px solid black;
        background: gray;
        color: white;
        padding: 7px 13px;
        margin-right: 12px;
        margin-left: 20px;
    }
</style>

