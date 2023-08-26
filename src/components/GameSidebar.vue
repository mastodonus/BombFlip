<template>
  <div class="sidebar"></div>
</template>

<script>
export default {
  name: "GameSidebar",
};
</script>

<style>
.sidebar {
  position: fixed;
  z-index: 1px;
  top: 0;
  left: 0;
  height: 100%;
  background-color: var(--theme-colour-darkest);
  width: 4rem;
  overflow-x: hidden;
}
</style>
