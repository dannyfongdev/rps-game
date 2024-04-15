<template>
  <div class="flex flex-col w-[314px] h-[428px] relative z-10 overflow-hidden">
    <div v-show="!playerChoice" class="relative p-5 mt-7 z-10">
      <img src="/images/bg-triangle.svg" alt="background triangle" />
    </div>
    <!-- Don't change the height of the grid container, or you will mess up the slide animations -->
    <div
      class="absolute grid grid-cols-2 grid-rows-[1fr_1fr_114px] items-center w-[314px] h-[428px] z-20"
    >
      <div :class="tokenPaper">
        <GameToken choice="paper" @click="play('paper')" />
      </div>
      <div :class="tokenScissors">
        <GameToken choice="scissors" @click="play('scissors')" />
      </div>
      <div :class="tokenRock">
        <GameToken choice="rock" @click="play('rock')" />
      </div>
      <div :class="tokenComputer">
        <GameToken :choice="computerChoice" :scale-in="computerChoice" />
      </div>
      <div
        class="border row-start-3 col-start-1 col-span-2 flex flex-col justify-center items-center h-[114px] -mt-24"
      >
        <p class="text-center text-4xl uppercase font-bold mb-6">
          {{ results }}
        </p>
        <button
          class="bg-blue-100 px-4 py-2 rounded-lg text-dark-text w-1/2 mx-auto"
          :class="showButton ? 'visible' : 'invisible'"
          @click="playAgain"
        >
          PLAY AGAIN
        </button>
      </div>
    </div>
  </div>
  <div></div>
</template>

<script>
import GameToken from "./GameToken.vue";
export default {
  components: { GameToken },
  props: {
    step: String,
  },
  emits: ["newScore"],
  data() {
    return {
      // game data
      computerChoice: "",
      playerChoice: "",
      computerScore: 0,
      playerScore: 0,
      results: "",
      theWinner: "",

      // for conditional showing
      showButton: false,

      // classes for styling
      position1:
        "border mr-auto row-start-1 col-start-1 transition-transform ease-in-out duration-500",
      position2:
        "border ml-auto row-start-1 col-start-2 transition-transform ease-in-out duration-500",
      position3:
        "border mx-auto row-start-2 col-start-1 col-span-2 transition-transform ease-in-out duration-500",
      tokenPaper: "hidden",
      tokenScissors: "hidden",
      tokenRock: "hidden",
      tokenComputer: "hidden",
    };
  },
  mounted() {
    this.newGame();
  },
  methods: {
    newGame() {
      this.tokenPaper = this.position1 + " cursor-pointer";
      this.tokenScissors = this.position2 + " cursor-pointer";
      this.tokenRock = this.position3 + " cursor-pointer";
      this.tokenComputer = "hidden";
    },
    play(choice) {
      this.playerChoice = choice;

      // move chosen token into position, slide others offcreen
      switch (choice) {
        case "rock":
          this.tokenPaper = this.position1 + " offscreen-l";
          this.tokenScissors = this.position2 + " offscreen-r";
          this.tokenRock = this.tokenRock + " from-3-to-1";
          break;
        case "paper":
          this.tokenScissors = this.position2 + " offscreen-r";
          this.tokenRock = this.position3 + " offscreen-b";
          break;
        case "scissors":
          this.tokenPaper = this.position1 + " offscreen-l";
          this.tokenScissors = this.position2 + " from-2-to-1";
          this.tokenRock = this.position3 + " offscreen-b";
          break;
      }

      // slide blank token into place
      this.tokenComputer = this.position2 + " p-blank-token";

      // pause before show computer's choice
      setTimeout(() => {
        this.computerPick();
      }, 500);
    },
    computerPick() {
      const computerOptions = ["rock", "paper", "scissors"];
      const choiceNumber = Math.floor(Math.random() * 3);
      this.computerChoice = computerOptions[choiceNumber];
      this.tokenComputer = this.position2;
      // console.log(this.computerChoice);

      this.winner(this.playerChoice, this.computerChoice);
    },
    winner(player, computer) {
      player = player.toLowerCase();
      computer = computer.toLowerCase();
      // console.log(player, computer);

      if (player === computer) {
        this.results = "DRAW";
        this.theWinner = "";
      } else if (
        (player === "rock" && computer === "scissors") ||
        (player === "paper" && computer === "rock") ||
        (player === "scissors" && computer === "paper")
      ) {
        this.playerScore++;
        this.results = "YOU WIN";
        this.theWinner = player;
      } else {
        this.computerScore++;
        this.results = "YOU LOSE";
        this.theWinner = computer;
      }
      // console.log(this.results);
      this.showButton = true;

      // send score back to parent component
      this.$emit("newScore", this.playerScore - this.computerScore);
    },
    playAgain() {
      this.showButton = false;
      this.playerChoice = "";
      this.computerChoice = "";
      this.results = "";
      this.newGame();
    },
  },
};
</script>

<style>
.offscreen-b {
  transform: translateY(calc(100vh));
}
.offscreen-l {
  transform: translateX(calc(-100vw));
}
.offscreen-r {
  transform: translateX(calc(100vw));
}
.from-3-to-1 {
  transform: translate(-92px, -158px);
}
.from-2-to-1 {
  transform: translateX(-184px);
}
.p-blank-token {
  padding: 2px;
}
</style>
