<template>
  <div class="">
    <div class="flex justify-between mb-20">
      <div class="flex flex-col items-center gap-6">
        <GameToken :choice="playerChoice" :winner="theWinner" class="" />
        <p>YOU PICKED</p>
      </div>
      <div class="flex flex-col items-center gap-6">
        <GameToken :choice="computerChoice" :winner="theWinner" class="" />
        <p>THE HOUSE PICKED</p>
      </div>
    </div>
    <div class="flex flex-col justify-center" v-show="showButton">
      <div class="text-center text-4xl uppercase font-bold mb-6">
        {{ result }}
      </div>
      <button
        class="bg-blue-100 px-4 py-2 rounded-lg text-dark-text w-1/2 mx-auto"
        @click="handleClick"
      >
        PLAY AGAIN
      </button>
    </div>
  </div>
</template>

<script>
import GameToken from "./GameToken.vue";
export default {
  props: {
    playerChoice: String,
    computerChoice: String,
    theWinner: String,
    result: String,
  },
  data() {
    return {
      showButton: false,
    };
  },
  components: { GameToken },
  emits: ["playAgain"],
  methods: {
    handleClick() {
      this.$emit("playAgain");
    },
  },
  mounted() {
    setTimeout(() => {
      this.showButton = true;
    }, 500);
  },
};
</script>
