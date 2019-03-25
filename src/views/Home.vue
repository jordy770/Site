<template>
  <div id="app">
    <AddGame v-on:add-game="addGame"/>
    <Games v-bind:games="games" v-on:del-game="deleteGame" v-on:edit-game="editGame"/>
    
  </div>
</template>

<script>
import Games from '../components/Games';
import AddGame from '../components/AddGame';
// import GameItem from '../components/GameItem';
import axios from 'axios';





export default {
  name: 'Home',
  components: {
    Games,
    // GameItem,
    AddGame
  },
  data() {
    return {
      games: []
    }
  },
  methods: {
    deleteGame(id){
      axios
      .delete(`http://51.68.188.157:8000/api/${id}`)
        .then(res => this.games = this.games.filter(game => game._id !== id) )
        .catch(err => console.log(err));
    },

    addGame(newGame) {
      const { title, studio, genre} = newGame;

      axios.post('http://51.68.188.157:8000/api/', {
        title,
        studio,
        genre
      })
        .then(res => this.games = [...this.games, res.data] )
        .catch(err => console.log(err));
    },

    editGame(editGame) {
      const {title, studio, genre} = editGame;

      axios.put(`http://51.68.188.157:8000/api/${editGame}`, {
        title,
        studio,
        genre
      })
        .then(res => this.games = this.games.filter(game => game._id !== id))
        .catch(err => console.log(err));
    },
  },

  created(){
    axios.get('http://51.68.188.157:8000/api/')
    .then(res => this.games = res.data.items)
    .catch(err => console.error());
  }

}
</script>


<style>
  * {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
  }

  body{
    font-family: Arial, Helvetica, sans-serif;
    line-height: 1.4;
  }

  .btn {
    display: inline-block;
    border: none;
    background: #555;
    color: #fff;
    padding: 7px 20px;
    cursor: pointer;
  }

  .btn:hover{
    background: #666;
  }
</style>
