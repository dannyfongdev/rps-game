<template>
  <div
    class="flex justify-between items-center h-[96px] w-[316px] border-4 border-header-outline rounded-lg p-6"
  >
    <div class="leading-[.85] text-lg cursor-pointer" @click="handleClick">
      ROCK<br />PAPER<br />SCISSORS<br />LIZARD<br />SPOCK
    </div>
    <div
      class="flex flex-col justify-center items-center rounded-md bg-white w-[86px] h-[72px] -mr-3"
    >
      <div class="text-score-text text-xs tracking-wider">SCORE</div>
      <div class="text-dark-text text-4xl font-black">{{ score }}</div>
    </div>
  </div>
</template>
<script>
export default {
  props: { score: Number },
  emits: ["toggle"],
  methods: {
    handleClick() {
      this.$emit("toggle");
    },
  },
};
</script>
