<script setup>
import TracklistDemo from "./components/TracklistDemo.vue";
import TayDoList from "./components/TayDoList.vue";
</script>

<template>
  <div class="components-container">
    <TracklistDemo class="component-box" />
    <TayDoList class="component-box" />
  </div>
</template>

<style scoped>
.components-container {
  display: flex;
  gap: 20px;
  padding: 0 10px;
}

.component-box {
  flex-grow: 1;
  min-width: 0;
}

@media (max-width: 768px) {
  .components-container {
    flex-direction: column;
  }
}
</style>
