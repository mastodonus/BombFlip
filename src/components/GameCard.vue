<template>
  <div class="game-card">
    <slot></slot>
  </div>
</template>

<script>
export default {
  name: "GameCard",
};
</script>

<style scoped>
.game-card {
  width: inherit;
  height: inherit;
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  border: 1px solid;
  border-radius: 4px;
  border-color: var(--theme-colour-lightest);
}
</style>
