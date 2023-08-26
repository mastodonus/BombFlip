<template>
  <div class="game-flip-card-container">
    <div class="game-flip-card" :class="{ 'is-flipped': this.flipped }">
      <GameCard class="game-flip-card-face is-front">
        <slot name="front"></slot>
      </GameCard>
      <GameCard class="game-flip-card-face is-back">
        <slot name="back"></slot>
      </GameCard>
    </div>
  </div>
</template>
<script>
import GameCard from "./GameCard.vue";

export default {
  name: "GameFlipCard",
  components: {
    GameCard,
  },
  props: {
    flipped: {
      type: Boolean,
      default: false,
    },
  },
};
</script>
<style scoped>
.game-flip-card-container {
  width: 100%;
  height: 100%;
  perspective: 1000px;
}
.game-flip-card {
  width: 100%;
  height: 100%;
  position: relative;
  transition: 0.5s transform ease-in;
  transform-style: preserve-3d;
}

.game-flip-card.is-flipped {
  transform: rotateY(180deg);
}

.game-flip-card-face {
  position: absolute;
  display: flex;
  align-items: center;
  justify-content: center;
  -webkit-backface-visibility: hidden;
  backface-visibility: hidden;
}

.game-flip-card-face.is-back {
  transform: rotateY(180deg);
}
</style>
