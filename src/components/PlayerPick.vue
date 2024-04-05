<template>
  <div class="relative w-[314px]">
    <div class="absolute p-12">
      <img src="/images/bg-triangle.svg" alt="background triangle" />
    </div>
    <div class="absolute flex flex-col justify-center items-center gap-[14px]">
      <div class="flex justify-between w-[314px]">
        <GameToken
          mode="pick"
          choice="paper"
          @click="play('paper')"
          delay="0"
        />
        <GameToken
          mode="pick"
          choice="scissors"
          @click="play('scissors')"
          delay="300"
        />
      </div>
      <div>
        <GameToken
          mode="pick"
          choice="rock"
          @click="play('rock')"
          delay="600"
        />
      </div>
    </div>
  </div>
</template>

<script>
import GameToken from "./GameToken.vue";
export default {
  components: { GameToken },
  emits: ["pick"],
  methods: {
    play(choice) {
      this.$emit("pick", choice);
    },
  },
};
</script>

<style>
@keyframes scale-up {
  0% {
    transform: scale(0);
  }
  100% {
    transform: scale(1);
  }
}

.animate-scale-up {
  animation: scale-up 0.5s ease-in-out forwards;
}
</style>
