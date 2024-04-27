<template>
  <div class="bg-transparent z-50" :class="animationClass">
    <img :src="imageURL" alt="game token" />
  </div>
</template>
<script>
export default {
  props: {
    choice: "",
    scaleIn: "",
    size: "",
    winner: "",
  },
  data() {
    return {};
  },
  computed: {
    imageURL() {
      if (!this.choice) {
        return "images/icon-blank.svg";
      }
      return "images/icon-" + this.choice + ".svg";
    },
    backgroundGradient() {
      return "gradient-" + this.choice;
    },
    animationClass() {
      // small means it is for user to pick
      // otherwise we are show what player and computer picked
      if (this.size === "small") {
        return "w-24 fade-in";
      } else {
        if (this.choice === this.winner) {
          return "w-32 lg:w-[200px] xl:w-[290px] animate-bounce";
        } else {
          return "w-32 lg:w-[200px] xl:w-[290px] scale-in";
        }
      }
    },
  },
};
</script>

<style scoped>
@keyframes kf-scale-in {
  0% {
    transform: scale(0);
  }
  100% {
    transform: scale(1);
  }
}
.scale-in {
  animation: kf-scale-in 500ms ease-in-out forwards;
}
@keyframes kf-fade-in {
  0% {
    opacity: 0;
  }
  100% {
    opacity: 1;
  }
}
.fade-in {
  animation: kf-fade-in 150ms ease-in-out forwards;
}
</style>
