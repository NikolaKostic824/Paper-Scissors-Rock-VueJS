<template>
  <div>
    <!-- Passing Data as Props in Head.vue -->
    <app-head :player="player" :computer="computer" :name="name"></app-head>
    <br>
    <!-- Input Field for Creating Player Name and Condition for Display if Game isn't Started and Start game on Pres Enter -->
    <input type="text" v-model="name" v-show="!game" @keyup.enter="game = true">
    <br>
    <!-- Setting Game Data on True and  Hide if Game is Started-->
    <button class="dugme" @click.prevent="game = true" v-show="!game">Lets start</button>
    <!-- Passing and Collecting Data from Items.vue and show if Game is Started(True)-->
    <app-items v-show="game"
               :player="player"
               :computer="computer"
               @increase="player = $event"
               @decrease="computer = $event"
               @playerReset="player = $event"
               @computerReset="computer = $event"></app-items>
  </div>

</template>

<script>
  //importing Components
  import Head from './components/Head'
  import Items from './components/Items'

  export default {
    data() {
      return {
        //Data for Props
        name: 'Player',
        player: 0,
        computer: 0,
        //Change to Start Game on Click or Enter
        game: false,
      }
    },
    //Adding Components to Tags
    components: {
      'app-head': Head,
      'app-items': Items
    }
  }
</script>

<style>
  /* Global  */
  body {
    background-color: #24272e;
    color: white;
    max-width: 500px;
    margin: 0 auto;
    box-sizing: border-box;
    text-align: center;
  }

  /* Button  */
  .dugme {
    width: 130px;
    height: 50px;
    color: orangered;
    background-color: #42b883;
    border: 3px solid blue;
    border-radius: 10px;
    font-weight: bold;
    font-size: medium;
    cursor: pointer;
  }

  /* Input */
  input {
    display: block;
    margin: 0 auto;
    width: 350px;
    height: 50px;
    font-size: 25px;
    background-color: #42b883;
    border: 3px solid blue;
    border-radius: 10px;
    color: orangered;
  }
</style>
