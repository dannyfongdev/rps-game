<template>
  <div class="h-svh w-svw flex items-center bg-slate-900/70">
    <div
      class="h-svh w-svw grid justify-center items-center bg-white fade-in p-4 md:w-[412px] md:h-[412px] md:mx-auto"
    >
      <div
        class="mx-auto text-3xl text-dark-text font-black md:w-full md:mr-auto"
      >
        RULES
      </div>
      <img
        src="/images/image-rules-bonus.svg"
        alt="rules"
        class="w-[90%] mx-auto mb-4 md:col-span-2"
      />
      <button
        class="mx-auto cursor-pointer md:row-start-1 md:col-start-2 focus:outline-0"
        @click="emitClose"
        ref="closeButton"
        @keydown.esc="emitClose"
      >
        <img
          class="ml-1 md:ml-[210px]"
          src="/images/icon-close.svg"
          alt="close"
        />
      </button>
    </div>
  </div>
</template>

<script>
export default {
  mounted() {
    this.$refs.closeButton.focus();
  },
  methods: {
    emitClose() {
      this.$emit("close");
    },
  },
  emits: ["close"],
};
</script>

<style scoped>
@keyframes kf-fade-in {
  0% {
    opacity: 0;
  }
  100% {
    opacity: 1;
  }
}
.fade-in {
  animation: kf-fade-in 250ms ease-in-out forwards;
}
</style>
