<template>
  <div class="flex justify-center items-center gap-10 p-10">
    <GameToken
      choice="rock"
      @click="play('rock')"
      class="bg-blue-100 px-4 py-2 rounded"
    />
    <GameToken
      choice="paper"
      @click="play('paper')"
      class="bg-blue-100 px-4 py-2 rounded"
    />
    <GameToken
      choice="scissors"
      @click="play('scissors')"
      class="bg-blue-100 px-4 py-2 rounded"
    />
  </div>
</template>

<script>
import GameToken from "./GameToken.vue";
export default {
  components: { GameToken },
  emits: ["pick"],
  methods: {
    play(choice) {
      this.$emit("pick", choice);
    },
  },
};
</script>
