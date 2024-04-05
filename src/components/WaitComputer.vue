<template>
  <div class="w-[314px]">
    <GameToken :choice="playerChoice" class="float-left" />
    <GameToken choice="blank" class="float-right" />
  </div>
</template>

<script>
import GameToken from "./GameToken.vue";
export default {
  props: {
    playerChoice: String,
  },
  data() {
    return {
      showComponent: true,
    };
  },
  components: { GameToken },
  mounted() {
    setTimeout(() => {
      this.handleClose();
    }, 2000);
  },
  emits: ["close"],
  methods: {
    handleClose(c) {
      this.$emit("close");
    },
  },
};
</script>
