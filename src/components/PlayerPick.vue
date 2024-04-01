<template>
  <h1>Rock, Paper, Scissors Game</h1>
  <div class="flex gap-1">
    <button @click="play('rock')" class="bg-blue-100 px-4 py-2 rounded">
      Rock
    </button>
    <button @click="play('paper')" class="bg-blue-100 px-4 py-2 rounded">
      Paper
    </button>
    <button @click="play('scissors')" class="bg-blue-100 px-4 py-2 rounded">
      Scissors
    </button>
  </div>
</template>

<script>
export default {
  emits: ["pick"],
  methods: {
    play(choice) {
      this.$emit("pick", choice);
    },
  },
};
</script>
