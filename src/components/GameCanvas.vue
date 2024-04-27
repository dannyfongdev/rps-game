<template>
  <div class="flex justify-center items-center h-[400px]">
    <!-- display the five choices for the player to pick -->
    <div v-show="showPicks" class="mx-auto">
      <div class="flex flex-col w-[314px] h-[314px] mb-8 relative z-10">
        <div class="relative p-5 z-10" v-show="!playerChoice">
          <img src="/images/bg-pentagon.svg" alt="background pentagon" />
        </div>

        <div
          class="absolute grid z-20 grid-cols-2 grid-rows-[1fr_1fr_1fr] justify-center items-center w-[314px] h-[314px]"
        >
          <div :class="tokenPaper">
            <GameToken size="small" choice="paper" @click="play('paper')" />
          </div>
          <div :class="tokenScissors">
            <GameToken
              size="small"
              choice="scissors"
              @click="play('scissors')"
            />
          </div>
          <div :class="tokenRock">
            <GameToken size="small" choice="rock" @click="play('rock')" />
          </div>
          <div :class="tokenLizard">
            <GameToken size="small" choice="lizard" @click="play('lizard')" />
          </div>
          <div :class="tokenSpock">
            <GameToken
              :size="tokenSize"
              choice="spock"
              @click="play('spock')"
            />
          </div>
        </div>
      </div>
    </div>

    <!-- display the results -->
    <div
      v-show="showResults"
      class="mx-auto grid grid-rows-2 gap-6 w-[314px] lg:grid-rows-1 lg:w-[800px] xl:w-[950px]"
    >
      <div
        :class="tokenPlayer"
        class="flex flex-col-reverse gap-4 lg:flex-col lg:gap-8"
      >
        <div class="mx-auto lg:text-xl">PLAYER PICKED</div>
        <div>
          <GameToken
            :choice="playerChoice"
            :winner="theWinner"
            scale-in="yes"
          />
        </div>
      </div>
      <div
        :class="tokenComputer"
        class="flex flex-col-reverse gap-4 lg:flex-col lg:gap-8"
      >
        <div class="mx-auto lg:text-xl">THE HOUSE PICKED</div>
        <div>
          <GameToken
            :choice="computerChoice"
            :winner="theWinner"
            scale-in="yes"
          />
        </div>
      </div>
      <div
        v-if="computerChoice"
        class="border-0 row-start-2 col-start-1 col-span-2 flex flex-col justify-center items-center lg:row-start-1 lg:col-start-2 lg:col-span-1"
      >
        <p
          v-show="showResults"
          class="text-center text-4xl uppercase font-bold mb-6"
        >
          {{ results }}
        </p>
        <button
          class="bg-blue-100 px-4 py-2 rounded-lg text-dark-text w-1/2 mx-auto cursor-pointer lg:w-[218px] lg:h-[46px]"
          :class="showResults ? 'visible' : 'invisible'"
          @click="playAgain"
        >
          PLAY AGAIN
        </button>
      </div>
    </div>
  </div>
</template>

<script>
import GameToken from "./GameToken.vue";
export default {
  components: { GameToken },
  props: {
    step: String,
    mode: String,
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
      showResults: false,
      showPicks: true,

      // position1 and position2 are the location for displaying the results
      position1:
        "border-0 mr-auto row-start-1 col-start-1 transition-transform ease-in-out duration-500",
      position2:
        "border-0 ml-auto row-start-1 col-start-2 transition-transform ease-in-out duration-500 lg:col-start-3", // lg: we put results in col-2

      // classes for positioning rock paper scissors lizard spock version for player to pick one
      positionA:
        "border-0 mx-auto row-start-1 col-start-1 col-span-2 transition-transform ease-in-out duration-500",
      positionB:
        "border-0 -mt-12 mr-auto row-start-2 col-start-1 transition-transform ease-in-out duration-500 delay-100",
      positionC:
        "border-0 -mt-12 ml-auto row-start-2 col-start-2 transition-transform ease-in-out duration-500 delay-100",
      positionD:
        "border-0 ml-12 mr-auto row-start-3 col-start-1 transition-transform ease-in-out duration-500 delay-200",
      positionE:
        "border-0 mr-12 ml-auto row-start-3 col-start-2 transition-transform ease-in-out duration-500 delay-200",

      // set this to apply tailwindCSS to the token, e.g. hidden, offscreen-x, etc.
      tokenPaper: "hidden",
      tokenScissors: "hidden",
      tokenRock: "hidden",
      tokenLizard: "hidden",
      tokenSpock: "hidden",

      // these are wrapper class that hold token and label for player and computer picks
      tokenPlayer: "hidden",
      tokenComputer: "hidden",
    };
  },
  computed: {
    tokenSize() {
      if (this.playerChoice) {
        // default is normal size. if player has chosen, we want to show normal size
        return "";
      } else {
        return "small";
      }
    },
  },
  mounted() {
    this.newGame();
  },
  methods: {
    newGame() {
      // five tokens layed out in shape of pentagon
      this.tokenScissors = this.positionA + " cursor-pointer";
      this.tokenSpock = this.positionB + " cursor-pointer";
      this.tokenPaper = this.positionC + " cursor-pointer";
      this.tokenLizard = this.positionD + " cursor-pointer";
      this.tokenRock = this.positionE + " cursor-pointer";
      this.showPicks = true;
    },
    play(choice) {
      // click should not have any effect if player has already chosen. newGame() will set playerChoice = ""
      if (this.playerChoice) {
        return;
      }

      this.playerChoice = choice;

      // slide tokens offcreen
      this.tokenScissors = this.positionA + " offscreen-t";
      this.tokenSpock = this.positionB + " offscreen-l";
      this.tokenPaper = this.positionC + " offscreen-r";
      this.tokenLizard = this.positionD + " offscreen-l";
      this.tokenRock = this.positionE + " offscreen-r";

      // slide blank token into place
      this.tokenPlayer = this.position1 + " p-blank-token";
      this.tokenComputer = this.position2 + " p-blank-token";

      // pause to let pick tokens animate out
      setTimeout(() => {
        this.computerPick();
        this.showPicks = false;
      }, 700);
    },
    computerPick() {
      const computerOptions = ["rock", "paper", "scissors", "lizard", "spock"];
      const choiceNumber = Math.floor(Math.random() * 5);
      this.computerChoice = computerOptions[choiceNumber];
      this.tokenComputer = this.position2;
      this.winner(this.playerChoice, this.computerChoice);
    },
    winner(player, computer) {
      player = player.toLowerCase();
      computer = computer.toLowerCase();

      if (player === computer) {
        this.results = "DRAW";
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
        this.results = "YOU WIN";
        this.theWinner = player;
      } else {
        this.computerScore++;
        this.results = "YOU LOSE";
        this.theWinner = computer;
      }

      this.showResults = true;

      // send score back to parent component
      this.$emit("newScore", this.playerScore - this.computerScore);
    },
    playAgain() {
      this.showResults = false;
      this.playerChoice = "";
      this.computerChoice = "";
      this.results = "";
      this.newGame();
    },
  },
};
</script>

<style>
.offscreen-t {
  transform: translateY(calc(-100vh));
}
.offscreen-b {
  transform: translateY(calc(100vh));
}
.offscreen-l {
  transform: translateX(calc(-100vw));
}
.offscreen-r {
  transform: translateX(calc(100vw));
}
.p-blank-token {
  padding: 2px;
}
</style>
