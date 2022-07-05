<template>
  <div
    @mousemove="$emit('mouse-move')"
    @mouseenter="$emit('mouse-enter')"
    @mouseleave="$emit('mouse-leave')"
  ></div>
</template>

<script>
export default {
  name: "Card",
  emits: ["mouse-move", "mouse-enter", "mouse-leave"],
};
</script>

<style scoped>
</style>