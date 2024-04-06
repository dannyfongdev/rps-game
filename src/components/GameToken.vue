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
    step: String,
    choice: String,
    winner: String,
    player: String,
  },
  data() {
    return {};
  },
  computed: {
    imageURL() {
      return "images/icon-" + this.choice + ".svg";
    },
    backgroundGradient() {
      return "gradient-" + this.choice;
    },
    animationClass() {
      let myClass = "";
      switch (this.step) {
        // user pick, scale from 0 to 100%, stagger in
        case "1":
          myClass = "cursor-pointer scale-in";
          // set delay so tokens stagger in
          if (this.choice === "rock") {
            myClass += " scale-delay-2";
          } else if (this.choice === "scissors") {
            myClass += " scale-delay-1";
          }
          break;

        // show user pick; slide from original position to left position
        case "2":
          if (this.choice === "blank") {
            // myClass = "absolute right-0";
          } else {
            myClass = "absolute left-0 slide-in-" + this.choice;
          }
          break;

        // show user pick and computer pick side-by-side
        case "3":
          if (this.player === "house") {
            myClass = "scale-in";
          }
          break;
      }
      // console.log(this.choice, myClass);
      return myClass;
    },
  },
};
</script>

<style scoped>
/* Step 1 */
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

/* Step 2 */
@keyframes kw-scissors {
  from {
    transform: translateX(140px);
  }
}
.slide-in-scissors {
  animation: kw-scissors 0.5s ease-in-out forwards;
}
@keyframes kw-rock {
  from {
    transform: translate(95px, 142px);
  }
}
.slide-in-rock {
  animation: kw-rock 0.5s ease-in-out forwards;
}
</style>
