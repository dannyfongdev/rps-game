<template>
  <div
    class="bg-transparent"
    :class="[winner === choice ? 'animate-bounce' : '']"
  >
    <div class="rounded-full p-4" :class="backgroundGradient" v-show="choice">
      <img
        class="w-24 bg-white rounded-full"
        :src="imageURL"
        alt="game token"
      />
    </div>
  </div>
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
