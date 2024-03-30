<template>
  <div>{{ choice }}</div>
  <img :src="imageURL" alt="game token" />
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
  },
};
</script>
