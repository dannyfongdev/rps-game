<template>
  <div class="h-svh w-svw grid justify-center items-center bg-white fade-in">
    <div class="mx-auto text-3xl text-dark-text font-black">RULES</div>
    <img src="/images/image-rules-bonus.svg" alt="rules" class="p-4" />
    <button
      class="mx-auto cursor-pointer"
      @click="emitClose"
      ref="closeButton"
      @keydown.esc="emitClose"
    >
      <img src="/images/icon-close.svg" alt="close" />
    </button>
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
