<template>
  <div class="">
    <div class="h-[100vh] grid grid-rows-[auto_1fr] gradient-board text-[#FFF]">
      <div class="">
        <Header :score="playerScore - computerScore" />
      </div>
      <div class="bg-red-100">
        <PlayerPick @pick="handlePick" v-show="playerChoice === ''" />
        <div v-show="playerChoice && computerChoice">
          <div class="flex">
            <GameToken :choice="playerChoice" />
            <GameToken :choice="computerChoice" />
          </div>
          <p class="">{{ result }}</p>
          <button
            class="bg-blue-100 px-4 py-2 rounded text-black"
            @click="playAgain"
          >
            PLAY AGAIN
          </button>
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
        this.result = "It's a draw!";
      } else if (
        (player === "rock" && computer === "scissors") ||
        (player === "paper" && computer === "rock") ||
        (player === "scissors" && computer === "paper")
      ) {
        this.playerScore++;
        this.result = "You win!";
      } else {
        this.computerScore++;
        this.result = "Computer wins!";
      }
    },
    playAgain() {
      this.playerChoice = "";
      this.computerChoice = "";
    },
  },
};
</script>
