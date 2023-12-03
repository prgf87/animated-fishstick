<template>
  <router-view />
</template>

<script lang="ts">
import { defineComponent, onMounted, watch } from 'vue';
import { useDarkMode, useTheme } from '@code-coaching/vuetiful';
import { useQuasar } from 'quasar';
import '@code-coaching/vuetiful/styles/all.css';
import '@code-coaching/vuetiful/css/overrides/quasar.css';
import './css/app.css';

export default defineComponent({
  name: 'App',
  setup() {
    const { autoModeWatcher, chosenMode, MODE } = useDarkMode();
    const { changeDataTheme } = useTheme();
    const $q = useQuasar();

    onMounted(() => {
      changeDataTheme('vuetiful'); // adds data-theme="vuetiful" to the <body> tag
      autoModeWatcher(); // automatically use the dark preference of the OS
      handleQuasarDarkMode(chosenMode.value);
    });

    const handleQuasarDarkMode = (mode: string) => {
      $q.dark.set(mode === MODE.DARK);
      if (mode === MODE.LIGHT) {
        document.body.classList.remove('body--light');
      } else {
        document.body.classList.remove('body--dark');
      }
    };

    watch(() => chosenMode.value, (newMode) => {
      handleQuasarDarkMode(newMode);
    });

    return {};
  },
});
</script>
