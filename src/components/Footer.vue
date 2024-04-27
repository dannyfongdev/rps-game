<template>
  <div class="flex justify-center">
    <button
      @click="handleClick"
      class="mx-auto border-2 px-10 py-2 border-header-outline rounded-lg lg:w-[128px] lg:h-[40px] lg:absolute lg:right-[30px] lg:bottom-[30px] lg:py-1"
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
