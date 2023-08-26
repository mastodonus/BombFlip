<template>
  <div class="game-tile-card">
    <div class="game-analysis-tile-inner">
      <GameCard class="card-face">
        <span>Value: {{ tile.value }}</span>
        <span>Bombs: {{ tile.bombs }}</span>
      </GameCard>
    </div>
  </div>
</template>

<script>
import GameCard from "./GameCard.vue";

export default {
  name: "GameAnalysisTile",
  components: {
    GameCard,
  },
  props: {
    tile: {
      type: Object,
      required: true,
    },
  },
};
</script>

<style scoped>
.game-tile-card {
  width: 90%;
  height: 90%;
}

.game-analysis-tile-inner {
  width: 100%;
  height: 100%;
  perspective: 1000px;
}

.card-face {
  background-color: var(--theme-colour-lightest);
}
</style>
