<template>
  <main class="gradient-board text-white h-svh w-svw overflow-hidden">
    <div
      class="flex flex-col justify-between min-h-[630px] max-h-[750px] lg:max-h-[900px]"
    >
      <Header @toggle="handleToggle" :score="theScore" />
      <GameCanvas @new-score="changeScore" />
      <Footer @rules="openRules" />
    </div>
  </main>
  <Rules v-if="showRules" @close="closeRules" class="absolute top-0 z-50" />
</template>

<script>
import Header from "./components/Header.vue";
import GameCanvas from "./components/GameCanvas.vue";
import Footer from "./components/Footer.vue";
import Rules from "./components/Rules.vue";

export default {
  components: {
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
