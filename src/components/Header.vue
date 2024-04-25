<template>
  <div
    class="flex justify-between items-center h-[96px] w-[316px] border-4 border-header-outline rounded-lg pl-6 pr-4 md:w-[700px] md:h-[150px] md:pl-8 md:pr-6"
  >
    <div class="leading-[.85] text-lg md:text-2xl md:leading-[.8]">
      ROCK<br />PAPER<br />SCISSORS<br />LIZARD<br />SPOCK
    </div>
    <div
      class="flex flex-col justify-center items-center rounded-md bg-white w-[86px] h-[72px] md:w-[152px] md:h-[100px] md:gap-0"
    >
      <div class="text-score-text text-xs tracking-wider md:text-xl">SCORE</div>
      <div class="text-dark-text text-4xl font-black md:text-5xl">
        {{ score }}
      </div>
    </div>
  </div>
</template>
<script>
export default {
  props: { score: Number },
};
</script>
