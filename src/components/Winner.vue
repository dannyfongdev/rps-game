<template>
  <div class="">
    <div class="grid grid-cols-2">
      <GameToken
        :choice="playerChoice"
        :winner="theWinner"
        class="row-start-1 col-start-1"
      />
      <div
        v-if="showButton === true"
        class="row-start-2 col-span-2 flex flex-col justify-center"
      >
        <p class="text-center">{{ result }}</p>
        <button
          class="bg-blue-100 px-4 py-2 rounded text-black w-8/12 mx-auto"
          @click="handleClick"
        >
          PLAY AGAIN
        </button>
      </div>
      <GameToken
        :choice="computerChoice"
        :winner="theWinner"
        class="row-start-1 col-start-2"
      />
    </div>
  </div>
</template>

<script>
import GameToken from "./GameToken.vue";
export default {
  props: {
    playerChoice: "",
    computerChoice: "",
    theWinner: "",
    result: "",
  },
  data() {
    return {
      showButton: false,
    };
  },
  components: { GameToken },
  emits: ["playAgain"],
  methods: {
    handleClick() {
      this.$emit("playAgain");
    },
  },
  mounted() {
    setTimeout(() => {
      this.showButton = true;
      // alert("I'm showing", this.showButton);
    }, 2000);
  },
};
</script>
