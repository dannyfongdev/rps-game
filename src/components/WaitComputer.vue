<template>
  <div class="flex justify-between w-[314px]">
    <p>This component will close after 2000ms.</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      showComponent: true,
    };
  },
  mounted() {
    setTimeout(() => {
      this.handleClose();
    }, 2000);
  },
  emits: ["close"],
  methods: {
    handleClose(c) {
      //   alert("I'm closing");
      this.$emit("close");
    },
  },
};
</script>
