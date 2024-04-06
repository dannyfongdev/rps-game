<template>
  <div class="w-[314px] h-[314px] relative flex flex-col z-10">
    <div class="p-12">
      <img src="/images/bg-triangle.svg" alt="background triangle" />
    </div>
    <div
      class="absolute z-20 flex flex-col justify-center items-center gap-[14px]"
    >
      <div class="flex justify-between w-[314px]">
        <GameToken step="1" choice="paper" @click="play('paper')" />
        <GameToken step="1" choice="scissors" @click="play('scissors')" />
      </div>
      <div>
        <GameToken step="1" choice="rock" @click="play('rock')" />
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
