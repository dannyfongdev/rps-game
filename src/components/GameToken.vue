<template>
  <div :class="backgroundGradient" v-if="choice">
    <div>{{ choice }}</div>
    <img :src="imageURL" alt="game token" />
  </div>
</template>

<script>
export default {
  props: {
    choice: String,
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
