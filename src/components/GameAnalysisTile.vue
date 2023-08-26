<template>
  <div class="game-tile-card">
    <div class="game-analysis-tile-inner">
      <GameCard class="card-face flex-column space-evenly">
        <span class="card-face-item flex-row space-evenly"
          ><SigmaIcon :size="18"></SigmaIcon>
          <span class="card-face-item-value">{{ tile.value }}</span></span
        >
        <span class="card-face-item flex-row space-evenly">
          <BombIcon :size="18"></BombIcon>
          <span class="card-face-item-value">{{ tile.bombs }}</span></span
        >
      </GameCard>
    </div>
  </div>
</template>

<script>
import GameCard from "./GameCard.vue";
import SigmaIcon from "vue-material-design-icons/Sigma.vue";
import BombIcon from "vue-material-design-icons/Bomb.vue";

export default {
  name: "GameAnalysisTile",
  components: {
    GameCard,
    SigmaIcon,
    BombIcon,
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
  border-color: var(--theme-colour-lightest);
}

.card-face-item {
  height: 50%;
  width: 100%;
  align-items: center;
}

.card-face-item-value {
  padding-bottom: 0.15rem;
}
</style>
