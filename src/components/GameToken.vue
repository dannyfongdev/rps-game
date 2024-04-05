<template>
  <!-- <div
    class="bg-transparent"
    :class="[winner === choice ? 'animate-bounce' : '']"
  > -->
  <img :src="imageURL" alt="game token" class="w-32" />
  <!-- </div> -->
</template>

<script>
export default {
  props: {
    choice: "",
    winner: "",
  },
  computed: {
    imageURL() {
      return "images/icon-" + this.choice + ".svg";
    },
    backgroundGradient() {
      return "gradient-" + this.choice;
    },
  },
};
</script>
