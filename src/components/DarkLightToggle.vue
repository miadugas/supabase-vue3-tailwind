<template>
  <div>
    <button
      class="pt-4 rounded-lg flex items-center justify-center transition-colors duration-500"
      :class="{
        'text-neutral-content': !isDark,
        'text-neutral-content': isDark,
      }"
      @click="toggleMode"
    >
      <span v-if="isDark">
        <!-- moon -->
        <svg
          xmlns="http://www.w3.org/2000/svg"
          class="fill-current w-10 h-10"
          viewBox="0 0 34 34"
        >
          <path
            d="M21.64,13a1,1,0,0,0-1.05-.14,8.05,8.05,0,0,1-3.37.73A8.15,8.15,0,0,1,9.08,5.49a8.59,8.59,0,0,1,.25-2A1,1,0,0,0,8,2.36,10.14,10.14,0,1,0,22,14.05,1,1,0,0,0,21.64,13Zm-9.5,6.69A8.14,8.14,0,0,1,7.08,5.22v.27A10.15,10.15,0,0,0,17.22,15.63a9.79,9.79,0,0,0,2.1-.22A8.11,8.11,0,0,1,12.14,19.73Z"
          />
        </svg>
      </span>
      <span v-else>
        <!-- sun -->
        <svg
          class="fill-current w-10 h-10"
          xmlns="http://www.w3.org/2000/svg"
          viewBox="0 0 34 34"
        >
          <path
            d="M5.64,17l-.71.71a1,1,0,0,0,0,1.41,1,1,0,0,0,1.41,0l.71-.71A1,1,0,0,0,5.64,17ZM5,12a1,1,0,0,0-1-1H3a1,1,0,0,0,0,2H4A1,1,0,0,0,5,12Zm7-7a1,1,0,0,0,1-1V3a1,1,0,0,0-2,0V4A1,1,0,0,0,12,5ZM5.64,7.05a1,1,0,0,0,.7.29,1,1,0,0,0,.71-.29,1,1,0,0,0,0-1.41l-.71-.71A1,1,0,0,0,4.93,6.34Zm12,.29a1,1,0,0,0,.7-.29l.71-.71a1,1,0,1,0-1.41-1.41L17,5.64a1,1,0,0,0,0,1.41A1,1,0,0,0,17.66,7.34ZM21,11H20a1,1,0,0,0,0,2h1a1,1,0,0,0,0-2Zm-9,8a1,1,0,0,0-1,1v1a1,1,0,0,0,2,0V20A1,1,0,0,0,12,19ZM18.36,17A1,1,0,0,0,17,18.36l.71.71a1,1,0,0,0,1.41,0,1,1,0,0,0,0-1.41ZM12,6.5A5.5,5.5,0,1,0,17.5,12,5.51,5.51,0,0,0,12,6.5Zm0,9A3.5,3.5,0,1,1,15.5,12,3.5,3.5,0,0,1,12,15.5Z"
          />
        </svg>
      </span>
    </button>
  </div>
</template>

<script lang="ts">
import { ref, nextTick } from "vue";

export default {
  setup() {
    const theme = ref(localStorage.getItem("theme") || "light");
    const isDark = ref(theme.value === "dark");

    const toggleMode = () => {
      isDark.value = !isDark.value;
      theme.value = isDark.value ? "dark" : "light";

      // Set initial theme
      document.documentElement.setAttribute("data-theme", theme.value);
      document.documentElement.classList.add("color-transition");

      nextTick(() => {
        setTimeout(() => {
          document.documentElement.classList.remove("color-transition");
        }, 1000);
      });

      // Store the selected theme
      localStorage.setItem("theme", theme.value);
    };

    return {
      isDark,
      toggleMode,
      theme,
    };
  },
};
</script>

<style scoped>
.bg-black {
  background-color: black;
}
.bg-white {
  background-color: white;
}
.text-black {
  color: black;
}
.text-white {
  color: white;
}
</style>
