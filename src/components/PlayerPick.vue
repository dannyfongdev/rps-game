<template>
  <div class="relative flex items-center justify-center">
    <div class="absolute p-12 w-[314px]">
      <img src="/images/bg-triangle.svg" alt="background triangle" />
    </div>
    <div
      class="absolute flex flex-col justify-center items-center gap-[14px] border-white _border"
    >
      <div class="flex justify-between w-[314px]">
        <GameToken choice="paper" @click="play('paper')" />
        <GameToken choice="scissors" @click="play('scissors')" />
      </div>
      <div class="">
        <GameToken choice="rock" @click="play('rock')" />
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
