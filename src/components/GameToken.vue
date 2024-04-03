<template>
  <div
    class="bg-transparent"
    :class="[winner === choice ? 'animate-bounce' : '']"
  >
    <div class="rounded-full p-4" :class="backgroundGradient" v-show="choice">
      <div v-show="false">{{ choice }}</div>
      <div class="bg-white rounded-full p-6 w-[100px] h-[100px] flex">
        <img class="" :src="imageURL" alt="game token" />
      </div>
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
