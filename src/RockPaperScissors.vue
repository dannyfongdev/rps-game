<template>
  <div class="flex justify-center items-center h-svh gradient-board">
    <div class="grid grid-rows-[auto_1fr_auto] max-h-[750px] text-white border">
      <div>
        <Header @toggle="handleToggle" :score="playerScore - computerScore" />
      </div>
      <div class="flex justify-center items-center h-[428px] border">
        <GameCanvas />
        <!-- <PlayerPick @pick="handlePick" v-if="playerChoice === ''" />
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
        /> -->
      </div>
      <div>
        <Footer @rules="openRules" />
      </div>
    </div>
  </div>
  <Rules v-if="showRules" @close="closeRules" class="absolute top-0 z-50" />
</template>

<script>
import GameToken from "./components/GameToken.vue";
import Header from "./components/Header.vue";
import GameCanvas from "./components/GameCanvas.vue";
import Footer from "./components/Footer.vue";
import PlayerPick from "./components/PlayerPick.vue";
import Winner from "./components/Winner.vue";
import WaitComputer from "./components/WaitComputer.vue";
import Rules from "./components/Rules.vue";

export default {
  components: {
    GameToken,
    Header,
    GameCanvas,
    Footer,
    PlayerPick,
    Winner,
    WaitComputer,
    Rules,
  },
  emits: ["toggle"],
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
    handleToggle() {
      this.$emit("toggle");
    },
  },
};
</script>
