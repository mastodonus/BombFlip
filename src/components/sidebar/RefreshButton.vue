<template>
  <RefreshIcon @click="this.refresh"></RefreshIcon>
</template>

<script>
import RefreshIcon from "vue-material-design-icons/Refresh.vue";

export default {
  name: "RefreshButton",
  components: {
    RefreshIcon,
  },
  methods: {
    refresh() {},
  },
};
</script>
