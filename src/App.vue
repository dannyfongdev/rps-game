<template>
  <h1>Rock, Paper, Scissors Game</h1>
  <div class="flex gap-1">
    <button @click="play('rock')" class="bg-blue-100 px-4 py-2 rounded">
      Rock
    </button>
    <button @click="play('paper')" class="bg-blue-100 px-4 py-2 rounded">
      Paper
    </button>
    <button @click="play('scissors')" class="bg-blue-100 px-4 py-2 rounded">
      Scissors
    </button>
  </div>

  <p class="">Moves Left: {{ 10 - moves }}</p>
  <p>{{ choiceStatus }}</p>
  <p class="">{{ result }}</p>
  <p class="">Player Score: {{ playerScore }}</p>
  <p class="">Computer Score: {{ computerScore }}</p>
</template>

<script>
export default {
  data() {
    return {
      playerScore: 0,
      computerScore: 0,
      moves: 0,
      result: "",
      choiceStatus: "Let's Play!",
    };
  },
  methods: {
    play(playerChoice) {
      const computerOptions = ["rock", "paper", "scissors"];
      const choiceNumber = Math.floor(Math.random() * 3);
      const computerChoice = computerOptions[choiceNumber];
      this.winner(playerChoice, computerChoice);
      this.moves++;
      if (this.moves === 10) {
        this.gameOver();
      }
    },
    winner(player, computer) {
      this.choiceStatus = "Computer plays " + computer;
      player = player.toLowerCase();
      computer = computer.toLowerCase();

      if (player === computer) {
        this.result = "It's a draw!";
      } else if (
        (player === "rock" && computer === "scissors") ||
        (player === "paper" && computer === "rock") ||
        (player === "scissors" && computer === "paper")
      ) {
        this.playerScore++;
        this.result = "You win!";
      } else {
        this.computerScore++;
        this.result = "Computer wins!";
      }
    },
    gameOver() {
      alert("Game Over!");
    },
  },
};
</script>
