<script setup>
import { ref, onMounted } from "vue";

const isVisible = ref(true);

onMounted(() => {
  setTimeout(() => {
    isVisible.value = false;
  }, 2000); // 2 seconds
});
</script>

<template>
  <div v-if="isVisible" class="loading-spinner">
    <h1 class="text-3xl font-bold text-green-500 mb-6 text-center">
      Heritage Homes
    </h1>
    <div class="spinner"></div>
  </div>
</template>

<style scoped>
.loading-spinner {
  display: flex;
  justify-content: space-evenly;
  align-items: center;
  width: 100%;
  height: 100vh;
  background-color: rgba(255, 255, 255, 1);
  position: fixed;
  top: 0;
  left: 0;
  z-index: 9999;
}

.spinner {
  border: 8px solid #f3f3f3;
  border-top: 8px solid #22c55e;
  border-radius: 50%;
  width: 75px;
  height: 75px;
  animation: spin 1s linear infinite;
}

@keyframes spin {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}
</style>
