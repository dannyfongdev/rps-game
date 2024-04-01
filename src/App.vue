<template>
  <div class="">
    <div class="h-[100vh] grid grid-rows-[auto_1fr] gradient-board text-[#FFF]">
      <div class="">
        <Header :score="playerScore - computerScore" />
      </div>
      <div class="bg-red-100">
        <PlayerPick @pick="handlePick" />
        <GameToken :choice="playerChoice" />
        <GameToken :choice="computerChoice" />
        <p class="">{{ result }}</p>
      </div>
      <div class="">
        <Footer />
      </div>
    </div>
  </div>
</template>

<script>
import GameToken from "./components/GameToken.vue";
import Header from "./components/Header.vue";
import Footer from "./components/Footer.vue";
import PlayerPick from "./components/PlayerPick.vue";
export default {
  components: {
    GameToken,
    Header,
    Footer,
    PlayerPick,
  },
  data() {
    return {
      playerScore: 0,
      computerScore: 0,
      moves: 0,
      result: "Let's Play!",
      computerChoice: "",
      playerChoice: "",
    };
  },
  methods: {
    handlePick(playerChoice) {
      this.playerChoice = playerChoice;
      const computerOptions = ["rock", "paper", "scissors"];
      const choiceNumber = Math.floor(Math.random() * 3);
      this.computerChoice = computerOptions[choiceNumber];
      this.winner(playerChoice, this.computerChoice);
      this.moves++;
      if (this.moves === 10) {
        this.gameOver();
      }
    },
    winner(player, computer) {
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
  },
};
</script>
