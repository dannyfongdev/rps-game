<template>
  <div class="gradient-board">
    <div
      class="h-[100vh] mx-auto grid grid-rows-[auto_1fr] text-[#FFF] justify-center items-center"
    >
      <div class="">
        <Header :score="playerScore - computerScore" />
      </div>
      <div class="">
        <PlayerPick @pick="handlePick" v-show="playerChoice === ''" />
        <Winner
          @playAgain="playAgain"
          v-show="playerChoice && computerChoice"
          :playerChoice
          :computerChoice
          :theWinner
          :result
        />
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
import Winner from "./components/Winner.vue";
export default {
  components: {
    GameToken,
    Header,
    Footer,
    PlayerPick,
    Winner,
  },
  data() {
    return {
      playerScore: 0,
      computerScore: 0,
      moves: 0,
      result: "Let's Play!",
      computerChoice: "",
      playerChoice: "",
      theWinner: "",
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
    },
    winner(player, computer) {
      player = player.toLowerCase();
      computer = computer.toLowerCase();

      if (player === computer) {
        this.result = "DRAW";
        this.theWinner = "";
      } else if (
        (player === "rock" && computer === "scissors") ||
        (player === "paper" && computer === "rock") ||
        (player === "scissors" && computer === "paper")
      ) {
        this.playerScore++;
        this.result = "YOU WIN";
        this.theWinner = player;
      } else {
        this.computerScore++;
        this.result = "YOU LOSE";
        this.theWinner = computer;
      }
    },
    playAgain() {
      this.playerChoice = "";
      this.computerChoice = "";
    },
  },
};
</script>
