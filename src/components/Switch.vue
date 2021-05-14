<template>
<label class="switch">
  <input @click="toggleTheme" type="checkbox" v-model="checked">
  <span class="slider round"></span>
</label>

</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'Switch',
  data() {
    return {
      theme: '',
      checked: false,
    };
  },
  methods: {
    toggleTheme() {
      this.theme = this.theme === 'darkMode' ? '' : 'darkMode';
      this.checked = this.theme === 'darkMode';
      document.documentElement.setAttribute('data-theme', this.theme);
      localStorage.setItem('theme', this.theme);
    },
  },
  mounted() {
    const localTheme = localStorage.getItem('theme') || '';
    document.documentElement.setAttribute('data-theme', localTheme);
    this.theme = localTheme === 'darkMode' ? 'darkMode' : '';
    this.checked = localTheme === 'darkMode';
  },
});

</script>

<style scoped lang="scss">
.switch {
  position: relative;
  display: inline-block;
  width: 60px;
  height: 34px;
}

.switch input {
  opacity: 0;
  width: 0;
  height: 0;
}

.slider {
  position: absolute;
  cursor: pointer;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: var(--background);
  -webkit-transition: .4s;
  transition: .4s;
}

.slider:before {
  position: absolute;
  content: "";
  height: 26px;
  width: 26px;
  left: 4px;
  bottom: 4px;
  background-color: var(--header-bg);
  -webkit-transition: .4s;
  transition: .4s;
}

input:checked + .slider {
  background-color: var(--switch-color);
}

input:focus + .slider {
  box-shadow: 0 0 1px var(--switch-color);
}

input:checked + .slider:before {
  -webkit-transform: translateX(26px);
  -ms-transform: translateX(26px);
  transform: translateX(26px);
}

/* Rounded sliders */
.slider.round {
  border-radius: 34px;
}

.slider.round:before {
  border-radius: 50%;
}
</style>
