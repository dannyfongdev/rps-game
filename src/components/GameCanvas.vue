<template>
  <div class="flex flex-col w-[314px] h-[314px] relative z-10 overflow-hidden">
    <div class="p-5 mt-7" v-show="false && step == 1">
      <img src="/images/bg-triangle.svg" alt="background triangle" />
    </div>
    <div
      class="grid grid-cols-2 grid-rows-2 items-center w-[314px] h-[314px] border absolute z-20"
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
      <div :class="tokenBlank">
        <GameToken choice="blank" />
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
  },
  emits: ["pick"],
  data() {
    return {
      computerChoice: "",
      playerChoice: "",
      position1:
        "border mr-auto row-start-1 col-start-1 transition-transform ease-in-out duration-500",
      position2:
        "border ml-auto row-start-1 col-start-2 transition-transform ease-in-out duration-500",
      position3:
        "border mx-auto row-start-2 col-start-1 col-span-2 transition-transform ease-in-out duration-500",
      tokenPaper: "hidden",
      tokenScissors: "hidden",
      tokenRock: "hidden",
      tokenBlank: "hidden",
    };
  },
  mounted() {
    // step 1, show choices for user to pick
    this.tokenPaper = this.position1;
    this.tokenScissors = this.position2;
    this.tokenRock = this.position3;
  },
  methods: {
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
      this.tokenBlank = this.position2 + " p-blank-token";

      // pause before show computer's choice
      setTimeout(() => {
        this.computerPick();
      }, 1500);

      // this.$emit("pick", choice);
    },
    computerPick() {
      const computerOptions = ["rock", "paper", "scissors"];
      const choiceNumber = Math.floor(Math.random() * 3);
      this.computerChoice = computerOptions[choiceNumber];
      console.log(this.computerChoice);

      // slide computer's choice into place
      switch (this.computerChoice) {
        case "paper":
          this.tokenBlank = "hidden";
          this.tokenPaper = this.position2;
          break;
        case "scissors":
          this.tokenBlank = "hidden";
          this.tokenScissors = this.position2;
          break;
        case "rock":
          this.tokenBlank = "hidden";
          this.tokenRock = this.position2;
          break;
      }

      // this.winner(this.playerChoice, this.computerChoice);
      // this.moves++;
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
