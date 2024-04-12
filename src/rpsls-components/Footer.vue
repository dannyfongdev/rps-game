<template>
  <div class="h-[96px] flex items-center md:relative">
    <button
      @click="handleClick"
      class="mx-auto border-2 px-10 py-2 border-header-outline rounded-lg md:absolute md:bottom-0 md:right-0"
    >
      RULES
    </button>
  </div>
</template>

<script>
export default {
  emits: ["rules"],
  methods: {
    handleClick() {
      this.$emit("rules");
    },
  },
};
</script>
