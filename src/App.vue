<template>
  <div class="gradient-board">
    <div
      class="mx-auto h-svh w- grid grid-rows-[auto_1fr] text-[#FFF] justify-center items-center"
    >
      <div>
        <Header :score="playerScore - computerScore" />
      </div>
      <div class="relative">
        <PlayerPick @pick="handlePick" v-if="playerChoice === ''" />
        <WaitComputer
          :playerChoice="playerChoice"
          @close="computerPick"
          v-if="playerChoice && !computerChoice"
        />
        <Winner
          @playAgain="playAgain"
          v-if="playerChoice && computerChoice"
          :playerChoice
          :computerChoice
          :theWinner
          :result
        />
      </div>
      <div>
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
import WaitComputer from "./components/WaitComputer.vue";

export default {
  components: {
    GameToken,
    Header,
    Footer,
    PlayerPick,
    Winner,
    WaitComputer,
  },
  data() {
    return {
      playerScore: 0,
      computerScore: 0,
      moves: 0,
      result: "",
      computerChoice: "",
      playerChoice: "",
      theWinner: "",
    };
  },
  methods: {
    handlePick(playerChoice) {
      this.playerChoice = playerChoice;
    },
    computerPick() {
      const computerOptions = ["rock", "paper", "scissors"];
      const choiceNumber = Math.floor(Math.random() * 3);
      this.computerChoice = computerOptions[choiceNumber];
      this.winner(this.playerChoice, this.computerChoice);
      this.moves++;
    },
    winner(player, computer) {
      player = player.toLowerCase();
      computer = computer.toLowerCase();
      // console.log(player, computer);

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
