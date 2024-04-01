<template>
  <div class="rounded-full p-4" :class="backgroundGradient" v-show="choice">
    <div v-show="false">{{ choice }}</div>
    <div class="bg-white rounded-full p-4">
      <img :src="imageURL" alt="game token" />
    </div>
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
