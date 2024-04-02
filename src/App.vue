<template>
  <div class="">
    <div
      class="h-[100vh] grid grid-rows-[auto_1fr] gradient-board text-[#FFF] justify-center items-center"
    >
      <div class="">
        <Header :score="playerScore - computerScore" />
      </div>
      <div class="">
        <PlayerPick @pick="handlePick" v-show="playerChoice === ''" />
        <div v-show="playerChoice && computerChoice" class="grid grid-cols-2">
          <GameToken
            :choice="playerChoice"
            :winner="theWinner"
            class="row-start-1 col-start-1"
          />
          <div class="row-start-2 col-span-2 flex flex-col justify-center">
            <p class="text-center">{{ result }}</p>
            <button
              class="bg-blue-100 px-4 py-2 rounded text-black w-8/12 mx-auto"
              @click="playAgain"
            >
              PLAY AGAIN
            </button>
          </div>
          <GameToken
            :choice="computerChoice"
            :winner="theWinner"
            class="row-start-1 col-start-2"
          />
        </div>
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
