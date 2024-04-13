<template>
  <div class="flex justify-center">
    <button
      @click="handleClick"
      class="mx-auto border-2 px-10 py-2 border-header-outline rounded-lg"
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
