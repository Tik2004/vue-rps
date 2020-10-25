<template>
  <div id="app">
    <h1>Rock-Paper-Scissors</h1>
    <h4>By Tigran Arshakyan</h4>
    <div class="billboard">
      <h2 style="margin:0" class="billboard--score">
        {{playerPoints}} - {{botPoints}}
      </h2>
    </div>
    <div v-if="gameStarted">
      <div v-if="playerWon">
        <img src="./assets/win.png" class="result-image">
        <h1>{{playerMove}} beats {{botMove}}</h1>
        <h1 class="win-text">You Won!</h1>
      </div>
      <div v-else-if="botWon">
        <img src="./assets/lose.png" class="result-image">
        <h1>{{playerMove}} is beaten by {{botMove}}</h1>
        <h1 class="loss-text">You Lost!</h1>
      </div>
      <div v-else>
        <img src="./assets/tie.png" class="result-image">
        <h1 class="tie-text">Tie!</h1>
      </div>
    </div>
    <div class="moves">
      <img @click="makeMove('rock')" src="./assets/rock.png">
      <img @click="makeMove('paper')" src="./assets/paper.png">
      <img @click="makeMove('scissor')" src="./assets/scissors.png">
    </div>  
    
  </div>
</template>

<script>

export default {
  name: 'App',
  data() {
    return {
      botPoints: 0,
      playerPoints: 0,
      playerMove: '',
      botMove: '',
      moves: ['rock','paper','scissor'],
      gameStarted: false,
      playerWon: false,
      botWon: false,
      tie: false
    }
  },
  methods : {
    makeMove : function(playerMove) {
      this.playerMove = playerMove
      this.botMove = this.moves[Math.floor(Math.random() * 3)]
      this.gameStarted = true
      switch (this.playerMove + this.botMove) {
        case 'rockscissor':
        case 'paperrock':
        case 'scissorpaper':  
          this.playerWon = true;
          this.botWon = false;
          this.tie = true;
          this.playerPoints += 1;
          break;
        case 'scissorrock':
        case 'rockpaper':
        case 'paperscissor':  
          this.playerWon = false;
          this.botWon = true;
          this.tie = false;
          this.botPoints += 1;
          break;
        default:
          this.playerWon = false;
          this.botWon = false;
          this.tie = true;          
          break;
      }
    }
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Open+Sans&display=swap');

body {
  background: #24272e;
  color: white;
}

#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  margin-top: 60px;
  font-family: 'Open Sans', Helvetica, Arial, sans-serif;  
}

.billboard {  
  border: 2px solid #f04e4e;
  max-width: 10rem;
  font-size: 1.4rem;
  padding: 0;
  margin: 0 auto;
  background: #f5e55a;
  color: #424141;
  border-radius: .5rem;
}

.moves img {
  margin: 1rem;
  border: 3px solid white;
  padding: .7rem;
  border-radius: 50%;  
}

.win-text {
  color: #9fec23;
}

.loss-text {
  color: #f54141;
}

.tie-text {
  color: #f0c435;
}

.result-image {
  margin-top: 1rem;
  animation: rotate-right 2s infinite alternate forwards;
}



@keyframes rotate-right {
  100% {
    filter: invert(0.3);
  }
}

</style>
