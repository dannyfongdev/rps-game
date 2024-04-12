<template>
  <div class="gradient-board min-h-[768px]">
    <div
      class="mx-auto h-svh w- grid grid-rows-[auto_1fr] text-[#FFF] justify-center items-center"
    >
      <div>
        <Header @toggle="handleToggle" :score="playerScore - computerScore" />
      </div>
      <div class="relative">
        <PlayerPick @pick="handlePick" v-if="playerChoice === ''" />
        <WaitComputer
          :playerChoice
          @close="computerPick"
          v-if="playerChoice && !computerChoice"
        />
        <WaitComputerShow
          :playerChoice
          :computerChoice
          @close="computerPickDone"
          v-if="playerChoice && computerChoice && !showWinner"
        />
        <Winner
          @playAgain="playAgain"
          v-if="showWinner"
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
import WaitComputerShow from "./rpsls-components/WaitComputerShow.vue";
import Rules from "./rpsls-components/Rules.vue";

export default {
  components: {
    GameToken,
    Header,
    Footer,
    PlayerPick,
    Winner,
    WaitComputer,
    WaitComputerShow,
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
      showWinner: false,
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
    computerPickDone() {
      this.showWinner = true;
      console.log("setting showWinner", this.showWinner);
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
        (player === "rock" && computer === "lizard") ||
        (player === "paper" && computer === "rock") ||
        (player === "paper" && computer === "spock") ||
        (player === "scissors" && computer === "paper") ||
        (player === "scissors" && computer === "lizard") ||
        (player === "lizard" && computer === "spock") ||
        (player === "lizard" && computer === "paper") ||
        (player === "spock" && computer === "rock") ||
        (player === "spock" && computer === "scissors")
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
      this.showWinner = "";
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
