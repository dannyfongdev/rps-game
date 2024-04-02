<template>
  <div
    class="flex flex-col justify-center items-center h-full bg-[url('/images/bg-triangle.svg')] bg-cover bg-center"
  >
    <div class="flex justify-between -_mt-10">
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
    <div class="-_mb-10">
      <GameToken
        choice="rock"
        @click="play('rock')"
        class="bg-blue-100 px-4 py-2 rounded"
      />
    </div>
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
