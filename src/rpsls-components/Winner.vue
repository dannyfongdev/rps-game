<template>
  <div class="grid grid-cols-2 w-[314px] h-[314px] lg:grid-cols-3 lg:w-[940px]">
    <div class="flex flex-col items-center gap-6 lg:flex-col-reverse">
      <GameToken
        :choice="playerChoice"
        :winner="theWinner"
        step="4"
        player="you"
      />
      <p class="scale-0 you-label-in">YOU PICKED</p>
    </div>
    <div class="flex flex-col items-center gap-6 lg:flex-col-reverse">
      <GameToken
        :choice="computerChoice"
        :winner="theWinner"
        step="4"
        player="house"
      />
      <p class="scale-0 house-label-in">THE HOUSE PICKED</p>
    </div>
    <div
      class="col-span-2 mt-20 lg:col-start-2 lg:row-start-1 lg:col-span-1 lg:mt-0"
    >
      <div class="flex flex-col justify-center">
        <div
          class="text-center text-4xl uppercase font-bold mb-6 scale-0 message-in"
        >
          {{ result }}
        </div>
        <button
          class="bg-blue-100 px-4 py-2 rounded-lg text-dark-text w-1/2 mx-auto"
          :class="showButton ? 'visible' : 'invisible'"
          @click="handleClick"
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
    // console.log(this.playerChoice, this.computerChoice);
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
