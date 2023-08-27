<template>
  <div class="game-tile-card">
    <GameFlipCard :flipped="this.tile?.flipped">
      <template v-slot:front>
        <span class="card-face card-face-hidden">
          <span v-if="this.tile.marked"><ShieldIcon></ShieldIcon></span>
          <span v-else>?</span>
        </span>
      </template>
      <template v-slot:back>
        <span
          class="card-face"
          :class="this.tile?.value > 0 ? 'success' : 'error'"
        >
          <span v-if="this.tile?.value > 0">{{ this.tile?.value }}</span>
          <span v-else><BombIcon></BombIcon></span>
        </span>
      </template>
    </GameFlipCard>
  </div>
</template>

<script>
import GameFlipCard from "./GameFlipCard.vue";
import BombIcon from "vue-material-design-icons/Bomb.vue";
import ShieldIcon from "vue-material-design-icons/Shield.vue";

export default {
  name: "GameTile",
  components: {
    GameFlipCard,
    BombIcon,
    ShieldIcon,
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
.game-tile-card:hover {
  cursor: pointer;
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
  border-color: var(--theme-colour-lightest) !important;
}

.card-face:hover {
  filter: contrast(90%);
  -webkit-filter: contrast(90%);
}

.success {
  background-color: white;
}

.error {
  background-color: var(--theme-colour-dark);
  border-color: var(--theme-colour-dark) !important;
}
</style>
