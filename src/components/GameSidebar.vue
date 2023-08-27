<template>
  <div class="sidebar">
    <ThemePicker class="sidebar-item"></ThemePicker>
    <RefreshButton class="sidebar-item"></RefreshButton>
  </div>
</template>

<script>
import ThemePicker from "./sidebar/ThemePicker.vue";
import RefreshButton from "./sidebar/RefreshButton.vue";

export default {
  name: "GameSidebar",
  components: {
    ThemePicker,
    RefreshButton,
  },
};
</script>

<style>
.sidebar {
  position: fixed;
  top: 0;
  left: 0;
  height: 100%;
  width: 4rem;
  z-index: 1px;
  background-color: var(--theme-colour-darkest);
  overflow-x: hidden;
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  align-items: center;
}

.sidebar-item {
  color: var(--theme-colour-light);
  margin-top: 1rem;
}

.sidebar-item:hover {
  cursor: pointer;
}
</style>
