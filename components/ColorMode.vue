<template>
    <div>
      <div class="icon-container">
        <LightbulbOutlineIcon
          class="icon"
          :class="{ active: colorMode.preference === 'light' }"
          @click="setColorMode('light')"
        />
        <Brightness4Icon
          class="icon"
          :class="{ active: colorMode.preference === 'dark' }"
          @click="setColorMode('dark')"
        />
        <MonitorIcon
          class="icon"
          :class="{ active: colorMode.preference === 'system' }"
          @click="setColorMode('system')"
        />
        <CloudIcon
          class="icon"
          :class="{ active: colorMode.preference === 'gray' }"
          @click="setColorMode('gray')"
        />
        
      </div>
      <div class="mt-5 w-full">
          <p class="description">Color mode: {{ colorMode.preference }}</p>
        </div>
    </div>
  </template>
  
  <script setup lang="ts">
  import LightbulbOutlineIcon from 'vue-material-design-icons/LightbulbOutline.vue'
  import Brightness4Icon from 'vue-material-design-icons/Brightness4.vue'
  import MonitorIcon from 'vue-material-design-icons/Monitor.vue'
  import CloudIcon from 'vue-material-design-icons/Cloud.vue'
  
  // Initialize colorMode
  const colorMode = useColorMode()
  
  // Method to set the color mode preference
  const setColorMode = (mode: string) => {
    colorMode.preference = mode
  }
  </script>
  
  <style scoped>
  .icon-container {
    display: flex;
    gap: 1rem;
  }
  
  .icon {
    cursor: pointer;
    font-size: 2rem;
    transition: color 0.3s;
  }
  
  .icon.active {
    color: var(--color-active); /* Define this variable in your global CSS */
  }
  </style>
  