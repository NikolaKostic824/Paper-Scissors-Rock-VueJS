<template>
  <div>
    <!-- Counter for Number of Turns -->
    <h3 style="color: orangered;">Number of turns: {{counter}}</h3>
    <!--Draw Calculation Display -->
    <h3 style="color: blue;">Number of draws:{{drawScore}}</h3>
    <!-- Battle Report -->
    <h2 style="color: #42b883;"> {{report}}</h2>
    <br/>
    <!-- Invoking Click Functions for All 3 Solutions -->
    <div class="items">
      <svg @click="rock">
        <use xlink:href="../../img/sprite.svg#icon-hand-grab-o"></use>
      </svg>
      <svg @click="scissors">
        <use xlink:href="../../img/sprite.svg#icon-hand-scissors-o"></use>
      </svg>
      <svg @click="paper">
        <use xlink:href="../../img/sprite.svg#icon-hand-paper-o"></use>
      </svg>
      <br>
      <!-- Button for Reset all Data -->
      <button class="dugme2" @click.prevent="startNew">Start new game!</button>
    </div>
  </div>
</template>

<script>

  export default {
    //Props from Parent
    props: ['player', 'computer'],
    data() {
      return {
        //Array for Possible Computer Choices
        items: ['rock', 'paper', 'scissors'],
        //First Display of Report
        report: 'Lets start!',
        //Starting Point for Counter who's Display Number of Turns
        counter: 0,
        //Starting Point for Counter who's Display Number of Draws
        drawScore: 0
      }
    },
    methods: {
      //Calculating Computer Choice from Array
      calculate() {
        return this.items[Math.floor(Math.random() * this.items.length)];
      },
      //Calculating Number of Draws
      draw() {
        this.drawScore = this.counter - (this.player + this.computer);
      },
      //Increase Counter on Click
      turns() {
        this.counter++;
      },
      //On SVG Click
      rock() {
        //Assign Random Item from Array to Variable
        let comp = this.calculate();
        //Invoking
        this.turns();
        console.log(comp);
        //Check who's Wins
        if (comp === 'rock') {
          //Report Update Based on conditions
          this.report = 'Comp chose Rock.Draw!';
        } else if (comp === 'paper') {
          this.report = 'Comp chose Paper.You lose!';
          //Increase Computer in Parent
          this.computer++;
          //Emitting new Value of Computer in parent
          this.$emit('decrease', this.computer);
        } else {
          this.report = 'Comp chose Scissors.You won!';
          //Increase Player in Parent
          this.player++;
          //Emitting new Value of Computer in parent
          this.$emit('increase', this.player);
        }
        //Invoking Draw Function for Calculating Number of Draws
        this.draw();
      },
      //On SVG Click Same as Rock Method
      paper() {
        let comp = this.calculate();
        this.turns();
        console.log(comp);
        if (comp === 'paper') {
          this.report = 'Comp chose Paper.Draw!';
        } else if (comp === 'scissors') {
          this.report = 'Comp chose Scissors.You lose!';
          this.computer++;
          this.$emit('decrease', this.computer);

        } else {
          this.report = 'Comp chose Rock.You won!';
          this.player++;
          this.$emit('increase', this.player);
        }
        this.draw();
      },
      //On SVG Click Same as Rock Method
      scissors() {
        let comp = this.calculate();
        this.turns();
        console.log(comp);
        if (comp === 'scissors') {
          this.report = 'Comp chose Scissors.Draw!';
        } else if (comp === 'rock') {
          this.report = 'Comp chose Rock.You Lose!';
          this.computer++;
          this.$emit('decrease', this.computer);
        } else {
          this.report = 'Comp chose Paper.You won!';
          this.player++;
          this.$emit('increase', this.player);
        }
        this.draw();
      },
      //Functionality of Start New Game Button. Rests all Data and Emitting Player and Computer as 0
      startNew() {
        if (confirm('Are you sure?')) {
          this.report = 'Lets start!';
          this.counter = 0;
          this.drawScore = 0;
          this.player = 0;
          this.computer = 0;
          this.$emit('playerReset', this.player);
          this.$emit('computerReset', this.computer);
        } else {
          return false;
        }
      }

    }
  }
</script>

<style scoped>

  /*Display of Items */
  .items {
    display: grid;
    grid-template-rows: auto;
    grid-template-columns: 1fr 1fr 1fr;
    grid-column-gap: 10px;
    justify-items: center;

  }

  /* SVG */
  svg {
    width: 70px;
    height: 70px;
    cursor: pointer;
    fill: white;
  }

  svg:hover {
    fill: #42b883;
    border: 2px solid #42b883;
  }

  /* Button 2 */
  .dugme2 {
    width: 130px;
    height: 50px;
    color: orangered;
    background-color: #42b883;
    border: 3px solid blue;
    border-radius: 10px;
    font-weight: bold;
    font-size: medium;
    cursor: pointer;
    margin-top: 20px;
  }
</style>
