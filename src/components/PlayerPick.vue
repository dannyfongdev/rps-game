<template>
  <div
    class="flex flex-col justify-center items-center gap-[14px] border-white _border"
  >
    <div class="flex justify-between w-[314px]">
      <GameToken choice="paper" @click="play('paper')" />
      <GameToken choice="scissors" @click="play('scissors')" />
    </div>
    <div class="">
      <GameToken choice="rock" @click="play('rock')" />
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
