<template>
  <div class="w-[314px] h-[314px]">
    <GameToken :choice="playerChoice" step="2" />
    <!-- <GameToken choice="blank" step="2" /> -->
  </div>
</template>

<script>
import GameToken from "./GameToken.vue";
export default {
  props: {
    playerChoice: String,
  },
  components: { GameToken },
  mounted() {
    setTimeout(() => {
      this.handleClose();
    }, 500);
  },
  emits: ["close"],
  methods: {
    handleClose() {
      this.$emit("close");
    },
  },
};
</script>
