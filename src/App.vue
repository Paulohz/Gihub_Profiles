<template>

    <Header msg="Github Profiles"/>
    <Main />
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import Header from './components/Header.vue';
import Main from './components/Main.vue';

export default defineComponent({
  name: 'App',
  components: {
    Header,
    Main,
  },
});
</script>

<style lang="scss">
    :root {
        --background: #f8f2f5;

        --header-bg: #e52e4d;
        --switch-color: #ffdf5d;

        --green: #33CC95;
        --blue: #5429cc;

        --blue-light: #6933ff;

        --text-title: #fff;
        --text-body: #312e2e;

        --shape: #ffffff;
    }

    [data-theme="darkMode"] {
    /* Variables for dark mode */
    --background: #090c10;
    --header-bg: #161b22;

    --text-title: #F0F6FC;
    --text-body: #f8f2f5;
  }

    * {
        margin: 0;
        padding: 0;
        box-sizing: border-box;
    }

    html {
        @media (max-width: 1080px) {
            font-size: 93.75%;
        }

        @media (max-width: 720px) {
            font-size: 87.5%;
        }
    }

    body {
        background: var(--background);
        -webkit-font-smoothing: antialised;
    }

    body, input, textarea, button {
        font-family: 'Poppins', sans-serif;
        font-weight: 400;
    }

    h1, h2, h3, h4, h5, h6, strong {
        font-weight: 600;
    }

    button {
        cursor: pointer;
    }
</style>
