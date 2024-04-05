<template>
  <!-- <div
    class="bg-transparent"
    :class="[winner === choice ? 'animate-bounce' : '']"
  > -->
  <img :src="imageURL" alt="game token" class="w-32" :class="animationClass" />
  <!-- </div> -->
</template>

<script>
export default {
  props: {
    choice: String,
    winner: String,
    mode: String,
    delay: "0",
  },
  computed: {
    imageURL() {
      return "images/icon-" + this.choice + ".svg";
    },
    backgroundGradient() {
      return "gradient-" + this.choice;
    },
    animationClass() {
      if (this.mode === "pick") {
        return (
          "cursor-pointer hover:opacity-50 inset-0 transform scale-0 animate-scale-up transition duration-300 ease-in-out animate-scale-up-" +
          this.delay
        );
      } else {
        return "";
      }
    },
  },
};
</script>

<style>
@keyframes scale-up {
  0% {
    transform: scale(0);
  }
  100% {
    transform: scale(1);
  }
}

.animate-scale-up-0 {
  animation: scale-up 0.5s ease-in-out forwards;
  animation-delay: 0;
}
.animate-scale-up-1 {
  animation: scale-up 0.5s ease-in-out forwards;
  animation-delay: 100ms;
}
.animate-scale-up-2 {
  animation: scale-up 0.5s ease-in-out forwards;
  animation-delay: 200ms;
}
</style>
