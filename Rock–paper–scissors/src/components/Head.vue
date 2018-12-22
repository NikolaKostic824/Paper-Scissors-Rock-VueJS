<template>
  <div>
    <h1><span style="color: mediumblue">Rock</span>–<span style="color:#42b883">paper</span>–<span
      style="color: orangered">scissors</span></h1>
    <div class="score">
      <!-- Using Props Name Computer and Player -->
      <h2><span style="color: mediumblue">{{name}}</span> score: <span style="color: mediumblue">{{player}}</span></h2>
      <h2 style="color: #42b883">VS</h2>
      <h2><span style="color: orangered">Computer</span> score: <span style="color: orangered">{{computer}}</span></h2>
    </div>
  </div>
</template>

<script>

  export default {
    //Props from parent
    props: ['player', 'computer', 'name']

  }
</script>

<style scoped>
  /* Div Style */
  .score {
    border: 5px solid #42b883;
    border-radius: 100px;
  }
</style>
