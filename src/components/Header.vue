<template>
  <header>

    <h1>{{ msg }}</h1>

    <Switch />

  </header>

</template>

<script lang="ts">
import { defineComponent } from 'vue';
import Switch from './Switch.vue';

export default defineComponent({
  name: 'Header',
  components: {
    Switch,
  },
  props: {
    msg: String,
  },
  data() {
    return {
      theme: '',
    };
  },
  methods: {
    toggleTheme() {
      this.theme = this.theme === 'darkMode' ? '' : 'darkMode';
      document.documentElement.setAttribute('data-theme', this.theme);
      localStorage.setItem('theme', this.theme);
    },
  },
  mounted() {
    const localTheme = localStorage.getItem('theme') || '';
    document.documentElement.setAttribute('data-theme', localTheme);
  },
});
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
header {
  background-color: var(--header-bg);
  padding: 50px;
  display: flex;
  justify-content: space-between;

  h1 {
    color: var(--text-title);
  }
}
</style>
