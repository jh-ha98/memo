<template>
  <div class="wrap">
    <div class="left">{{ props.left }}</div>
    <div class="right">{{ props.right }}</div>
  </div>
</template>

<script setup lang="ts">
const props = defineProps<{ right: any, left: any }>();
</script>

<style scoped>
.wrap {
  display: flex;
  height: 100%;
}

.left,
.right {
  flex: 50%;
}
.left {
  border-right: 1px black solid;
}
</style>
