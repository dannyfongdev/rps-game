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
          delay="1"
        />
      </div>
      <div>
        <GameToken mode="pick" choice="rock" @click="play('rock')" delay="2" />
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
