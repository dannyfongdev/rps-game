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
        <Footer @rules="openRules" />
      </div>
    </div>
  </div>
  <Rules v-if="showRules" @close="closeRules" class="absolute top-0 z-50" />
</template>

<script>
import GameToken from "./rpsls-components/GameToken.vue";
import Header from "./rpsls-components/Header.vue";
import Footer from "./rpsls-components/Footer.vue";
import PlayerPick from "./rpsls-components/PlayerPick.vue";
import Winner from "./rpsls-components/Winner.vue";
import WaitComputer from "./rpsls-components/WaitComputer.vue";
import Rules from "./rpsls-components/Rules.vue";

export default {
  components: {
    GameToken,
    Header,
    Footer,
    PlayerPick,
    Winner,
    WaitComputer,
    Rules,
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
      showRules: false,
    };
  },
  mounted() {
    // this.$refs.rulesDialog.showModal();
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
    closeRules() {
      this.showRules = false;
    },
    openRules() {
      this.showRules = true;
    },
  },
};
</script>
