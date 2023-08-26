<template>
  <div class="game-tile-card">
    <GameFlipCard :flipped="this.tile?.flipped">
      <template v-slot:front>
        <span class="card-face card-face-hidden">?</span>
      </template>
      <template v-slot:back>
        <span
          class="card-face"
          :class="this.tile?.value > 0 ? 'success' : 'error'"
          >{{ this.tile?.value }}</span
        >
      </template>
    </GameFlipCard>
  </div>
</template>

<script>
import GameFlipCard from "./GameFlipCard.vue";

export default {
  name: "GameTile",
  components: {
    GameFlipCard,
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
.card-face {
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: space-around;
}

.card-face-hidden {
  background-color: var(--theme-colour-lightest);
}

.card-face:hover {
  background-color: var(--theme-colour-light);
}

.success {
  background-color: white;
}

.error {
  background-color: var(--theme-colour-dark);
}
</style>
