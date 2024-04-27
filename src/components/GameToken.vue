<template>
  <div class="bg-transparent z-50" :class="sizeClass">
    <img
      :src="imageURL"
      alt="game token"
      :class="animationClass + ' ' + sizeClass"
    />
  </div>
</template>
<script>
export default {
  props: {
    choice: "",
    scaleIn: "",
    size: "",
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
      if (!this.scaleIn) {
        return "";
      } else {
        return "scale-in";
      }
    },
    sizeClass() {
      if (this.size === "small") {
        return "w-24";
      } else {
        return "w-32 lg:w-[200px] xl:w-[290px]";
      }
    },
  },
};
</script>

<style scoped>
/* scale from 0 to 1 for computer choice */
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
.scale-delay-1 {
  animation-delay: 100ms;
}
.scale-delay-2 {
  animation-delay: 200ms;
}
</style>
