<template>
  <div class="sidebar">
    <ThemePicker class="sidebar-item"></ThemePicker>
  </div>
</template>

<script>
import ThemePicker from "./sidebar/ThemePicker.vue";
export default {
  name: "GameSidebar",
  components: {
    ThemePicker,
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
  padding-top: 1rem;
  background-color: var(--theme-colour-darkest);
  overflow-x: hidden;
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  align-items: center;
}

.sidebar-item {
  color: var(--theme-colour-light);
}

.sidebar-item:hover {
  cursor: pointer;
}
</style>
