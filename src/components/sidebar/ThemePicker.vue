<template>
  <PaletteIcon @click="this.cycleTheme"></PaletteIcon>
</template>

<script>
import PaletteIcon from "vue-material-design-icons/Palette.vue";
export default {
  name: "ThemePicker",
  components: {
    PaletteIcon,
  },
  data() {
    return {
      theme: null,
      themes: ["dark", "ocean"],
    };
  },
  mounted() {
    this.setTheme(this.themes[0]);
  },
  methods: {
    cycleTheme() {
      let nextTheme = this.themes.indexOf(this.theme) + 1;
      if (nextTheme > this.themes.length - 1) {
        nextTheme = 0;
      }

      this.setTheme(this.themes[nextTheme]);
    },
    setTheme(theme) {
      this.theme = theme;
      document.documentElement.setAttribute("data-theme", this.theme);
    },
  },
};
</script>
