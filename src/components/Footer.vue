<template>
  <div class="flex justify-center max-w-[1440px] lg:justify-end lg:mr-8">
    <a
      @click="handleClick"
      class="border-2 px-10 py-2 border-header-outline rounded-lg cursor-pointer"
    >
      RULES
    </a>
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
