<template>
  <div class="">
    <div class="flex justify-between mb-20">
      <div class="flex flex-col items-center gap-6">
        <GameToken
          :choice="playerChoice"
          :winner="theWinner"
          step="3"
          player="you"
        />
        <p class="scale-0 you-label-in">YOU PICKED</p>
      </div>
      <div class="flex flex-col items-center gap-6">
        <GameToken
          :choice="computerChoice"
          :winner="theWinner"
          step="3"
          player="house"
        />
        <p class="scale-0 house-label-in">THE HOUSE PICKED</p>
      </div>
    </div>
    <div class="flex flex-col justify-center">
      <div
        class="text-center text-4xl uppercase font-bold mb-6 scale-0 message-in"
      >
        {{ result }}
      </div>
      <button
        v-show="showButton"
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
    }, 1500);
  },
};
</script>

<style scoped>
@keyframes kf-scale {
  0% {
    transform: scale(0);
  }
  100% {
    transform: scale(1);
  }
}
.message-in {
  animation: kf-scale 250ms ease-in-out forwards;
  animation-delay: 1s;
}

.you-label-in {
  animation: kf-scale 0ms ease-in-out forwards;
  animation-delay: 0.1s;
}
.house-label-in {
  animation: kf-scale 0ms ease-in-out forwards;
  animation-delay: 0.6s;
}
</style>
