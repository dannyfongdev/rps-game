<template>
  <RockPaperScissorsLizardSpock v-if="showLizardSpock" @toggle="toggleGame" />
  <RockPaperScissors v-if="showLizardSpock === false" @toggle="toggleGame" />
</template>

<script>
import RockPaperScissors from "./RockPaperScissors.vue";
import RockPaperScissorsLizardSpock from "./RockPaperScissorsLizardSpock.vue";

export default {
  components: {
    RockPaperScissors,
    RockPaperScissorsLizardSpock,
  },
  data() {
    return {
      showLizardSpock: false,
    };
  },
  methods: {
    toggleGame() {
      console.log(this.showLizardSpock);
      this.showLizardSpock = !this.showLizardSpock;
    },
  },
};
</script>
