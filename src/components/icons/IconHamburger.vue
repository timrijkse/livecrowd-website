<script setup lang="ts">
const props = defineProps<{
  isOpen: boolean
}>()
</script>

<template>
  <div class="icon-hamburger" :class="{ open: props.isOpen }">
    <span class="line"></span>
    <span class="line"></span>
    <span class="line"></span>
  </div>
</template>

<style scoped>
.icon-hamburger {
  position: relative;
  width: 29px;
  height: 29px;
}

.line {
  transition: transform 0.3s ease-in-out;
  position: absolute;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%);
  display: block;
  width: 100%;
  height: 2px;
  background-color: var(--color-navigation);
}

.line:nth-child(1) {
  transform: translate(-50%, calc(-50% - 8px)) rotate(0deg);
}

.line:nth-child(2) {
  transform: translate(-50%, calc(-50% + 8px)) rotate(0deg);
  background-color: green;
}

.open .line:nth-child(1) {
  transform: translate(-50%, -50%) rotate(45deg);
}

.open .line:nth-child(2) {
  transform: translate(-50%, -50%) rotate(-45deg);
}

.open .line:nth-child(3) {
  transform: scale(0);
}
</style>
