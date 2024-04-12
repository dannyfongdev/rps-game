<template>
  <div
    class="flex justify-between items-center h-[96px] w-[314px] border-4 border-header-outline rounded-lg mt-8 mb-8 p-6 lg:w-[700px] lg:h-[150px]"
  >
    <div class="leading-[.85] text-lg cursor-pointer" @click="handleClick">
      ROCK<br />PAPER<br />SCISSORS<br />LIZARD<br />SPOCK
    </div>
    <div
      class="flex flex-col justify-center items-center rounded-lg bg-white w-[86px] h-[72px] -mr-3 lg:h-[110px] lg:w-[150px]"
    >
      <div class="text-score-text text-xs tracking-wider lg:text-lg lg:-mt-2">
        SCORE
      </div>
      <div
        class="text-dark-text text-4xl font-black lg:text-7xl lg:leading-[.7]"
      >
        {{ score }}
      </div>
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
