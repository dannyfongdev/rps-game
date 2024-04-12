<template>
  <div class="w-[314px] h-[314px] relative flex flex-col z-10 mx-auto">
    <div class="p-12 md:w-[472px] md:self-center">
      <img src="/images/bg-pentagon.svg" alt="background pentagon" />
    </div>
    <div
      class="absolute z-20 flex flex-col justify-center items-center md:w-[472px] md:self-center"
    >
      <div class="mx-auto">
        <GameToken step="1" choice="scissors" @click="play('scissors')" />
      </div>
      <div class="flex justify-between w-[314px] -mt-6 md:w-[472px]">
        <GameToken step="1" choice="spock" @click="play('spock')" />
        <GameToken step="1" choice="paper" @click="play('paper')" />
      </div>
      <div
        class="flex justify-between w-[214px] mt-6 md:w-[342px] md:self-center"
      >
        <GameToken step="1" choice="lizard" @click="play('lizard')" />
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
