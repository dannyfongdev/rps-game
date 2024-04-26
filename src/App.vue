<template>
  <div class="flex justify-center items-center h-svh gradient-board">
    <div
      class="grid grid-rows-[auto_1fr_auto] max-h-[750px] text-white border-0"
    >
      <div>
        <Header @toggle="handleToggle" :score="theScore" />
      </div>
      <div class="flex justify-center items-center h-[428px] border-0">
        <GameCanvas mode="rpsls" @new-score="changeScore" />
      </div>
      <div>
        <Footer @rules="openRules" />
      </div>
    </div>
  </div>
  <Rules v-if="showRules" @close="closeRules" class="absolute top-0 z-50" />
</template>

<script>
import GameToken from "./components/GameToken.vue";
import Header from "./components/Header.vue";
import GameCanvas from "./components/GameCanvas.vue";
import Footer from "./components/Footer.vue";
import Rules from "./components/Rules.vue";

export default {
  components: {
    GameToken,
    Header,
    GameCanvas,
    Footer,
    Rules,
  },
  emits: ["toggle"],
  data() {
    return {
      theScore: 0,
      showRules: false,
    };
  },
  mounted() {
    // this.$refs.rulesDialog.showModal();
  },
  methods: {
    changeScore(newScore) {
      // delay so that score doesn't change before computer token is shown
      setTimeout(() => {
        this.theScore = newScore;
      }, 500);
    },
    closeRules() {
      this.showRules = false;
    },
    openRules() {
      this.showRules = true;
    },
    handleToggle() {
      this.$emit("toggle");
    },
  },
};
</script>
