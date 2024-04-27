<template>
  <div :class="wrapperClass">
    <!-- if playChoice is empty, game state is player pick -->
    <div v-show="!playerChoice" class="relative p-5 z-10">
      <img src="/images/bg-pentagon.svg" alt="background pentagon" />
    </div>

    <div :class="gameContainerClass">
      <div :class="tokenPaper">
        <GameToken :size="tokenSize" choice="paper" @click="play('paper')" />
      </div>
      <div :class="tokenScissors">
        <GameToken
          :size="tokenSize"
          choice="scissors"
          @click="play('scissors')"
        />
      </div>
      <div :class="tokenRock">
        <GameToken :size="tokenSize" choice="rock" @click="play('rock')" />
      </div>
      <div :class="tokenLizard">
        <GameToken :size="tokenSize" choice="lizard" @click="play('lizard')" />
      </div>
      <div :class="tokenSpock">
        <GameToken :size="tokenSize" choice="spock" @click="play('spock')" />
      </div>
      <div
        :class="tokenPlayer"
        class="flex flex-col-reverse gap-4 lg:flex-col lg:gap-8"
      >
        <div class="mx-auto lg:text-xl">PLAYER PICKED</div>
        <div>
          <GameToken :choice="playerChoice" :scale-in="playerChoice" />
        </div>
      </div>
      <div
        :class="tokenComputer"
        class="flex flex-col-reverse gap-4 lg:flex-col lg:gap-8"
      >
        <div class="mx-auto lg:text-xl">THE HOUSE PICKED</div>
        <div>
          <GameToken :choice="computerChoice" :scale-in="computerChoice" />
        </div>
      </div>
    </div>
    <div
      v-if="computerChoice"
      class="absolute z-40 bottom-0 border-0 row-start-3 col-start-1 col-span-2 flex flex-col justify-center items-center w-[314px] h-[114px] lg:w-[800px] lg:bottom-[280px] xl:w-[950px] xl:bottom-[240px]"
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

      // position1 and position2 are the location for displaying the results
      position1:
        "border-0 mr-auto row-start-1 col-start-1 transition-transform ease-in-out duration-500",
      position2:
        "border-0 ml-auto row-start-1 col-start-2 transition-transform ease-in-out duration-500",

      // classes for positioning rock paper scissors lizard spock version for player to pick one
      positionA:
        "border-0 mx-auto row-start-1 col-start-1 col-span-2 transition-transform ease-in-out duration-500",
      positionB:
        "border-0 -mt-12 mr-auto row-start-2 col-start-1 transition-transform ease-in-out duration-500",
      positionC:
        "border-0 -mt-12 ml-auto row-start-2 col-start-2 transition-transform ease-in-out duration-500",
      positionD:
        "border-0 ml-12 mr-auto row-start-3 col-start-1 transition-transform ease-in-out duration-500",
      positionE:
        "border-0 mr-12 ml-auto row-start-3 col-start-2 transition-transform ease-in-out duration-500",

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
    wrapperClass() {
      // if playerChoice is empty, then we are in the player pick state
      // Don't change the height of the container, or you will mess up the slide animations
      if (!this.playerChoice) {
        return "flex flex-col w-[314px] h-[314px] relative z-10";
      } else {
        return "flex flex-col justify-center w-[314px] h-[314px] relative z-10 overflow-visible lg:w-[800px] xl:w-[950px] lg:h-[600px]";
      }
    },
    gameContainerClass() {
      if (!this.playerChoice) {
        return "absolute grid z-20 grid-cols-2 grid-rows-[1fr_1fr_1fr] justify-center items-center w-[314px] h-[314px]";
      } else {
        return "absolute grid z-20 grid-cols-2 grid-rows-[1fr_1fr_1fr] justify-center items-center w-[314px] h-[314px]  lg:w-[800px] xl:w-[950px]";
      }
    },
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
      this.tokenPlayer = "hidden";
      this.tokenComputer = "hidden";
    },
    play(choice) {
      // click should not have any effect if player has already chosen
      // newGame() will set playerChoice = ""
      if (this.playerChoice) {
        return;
      }

      this.playerChoice = choice;

      // slide tokens offcreen

      this.tokenScissors = this.positionA + " offscreen-r";
      this.tokenSpock = this.positionB + " offscreen-l";
      this.tokenPaper = this.positionC + " offscreen-r";
      this.tokenLizard = this.positionD + " offscreen-l";
      this.tokenRock = this.positionE + " offscreen-r";

      // slide blank token into place
      this.tokenPlayer = this.position1 + " p-blank-token";
      this.tokenComputer = this.position2 + " p-blank-token";

      // pause before show computer's choice
      setTimeout(() => {
        this.computerPick();
      }, 500);
    },
    computerPick() {
      const computerOptions = ["rock", "paper", "scissors", "lizard", "spock"];
      const choiceNumber = Math.floor(Math.random() * 5);
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
      // show results after computer pick is shown, need delay
      setTimeout(() => {
        this.showResults = true;
      }, 700);

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
.offscreen-b {
  transform: translateY(calc(100vh));
}
.offscreen-l {
  transform: translateX(calc(-100vw));
}
.offscreen-r {
  transform: translateX(calc(100vw));
}
.from-a-to-1 {
  transform: translateX(-92px);
  @media (min-width: 1024px) {
    transform: translateX(-330px);
  }
}
.from-b-to-1 {
  transform: translateY(-82px);
  @media (min-width: 1024px) {
    transform: translateY(-244px);
  }
}
.from-c-to-1 {
  transform: translate(-184px, -80px);
  @media (min-width: 1024px) {
    transform: translate(-658px, -244px);
  }
}
.from-d-to-1 {
  transform: translate(-48px, -212px);
  @media (min-width: 1024px) {
    transform: translate(-48px, -534px);
  }
}
.from-e-to-1 {
  transform: translate(-156px, -212px);
  @media (min-width: 1024px) {
    transform: translate(-610px, -534px);
  }
}
.p-blank-token {
  padding: 2px;
}
</style>
