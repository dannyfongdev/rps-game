<template>
  <div class="h-[96px] flex items-center lg:relative">
    <button
      @click="handleClick"
      class="mx-auto border-2 px-10 py-2 border-header-outline rounded-lg lg:absolute lg:bottom-0 lg:right-0"
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
