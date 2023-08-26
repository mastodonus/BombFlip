<template>
  <div class="app-container">
    <GameSidebar></GameSidebar>
    <div class="game-board-container">
      <GameBoard></GameBoard>
    </div>
  </div>
</template>

<script>
import GameSidebar from "./components/GameSidebar.vue";
import GameBoard from "./components/GameBoard.vue";

export default {
  name: "App",
  components: {
    GameSidebar,
    GameBoard,
  },
};
</script>

<style>
body {
  width: 100%;
  height: 100%;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: var(--theme-colour-font);
  background-color: var(--theme-colour-dark);
}

.app-container {
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  min-width: 700px;
  min-height: 700px;
}

.game-board-container {
  display: flex;
  justify-content: space-around;
  width: 40%;
  min-width: 400px;
  height: 100%;
  min-height: 400px;
}

:root {
  color: var(--theme-colour-font);
  background-color: var(--theme-colour-dark);
}

html[data-theme="dark"] {
  --theme-colour-darkest: #2c3333;
  --theme-colour-dark: #2e4f4f;
  --theme-colour-light: #0e8388;
  --theme-colour-lightest: #cbe4de;
  --theme-colour-font: black;
}

html[data-theme="ocean"] {
  --theme-colour-darkest: #03001c;
  --theme-colour-dark: #3b466e;
  --theme-colour-light: #5b8fb9;
  --theme-colour-lightest: #b6eada;
  --theme-colour-font: black;
}
</style>
