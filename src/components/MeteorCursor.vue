<template>
  <div class="meteor-cursor" aria-hidden="true">
    <span class="meteor-pointer" :class="{ visible: pointer.visible }" :style="{ left: `${pointer.x}px`, top: `${pointer.y}px` }"><b>✦</b></span>
    <i v-for="meteor in meteors" :key="meteor.id" :style="{ left: `${meteor.x}px`, top: `${meteor.y}px`, '--size': `${meteor.size}px`, '--rotate': `${meteor.rotate}deg` }" />
  </div>
</template>

<script setup>
const meteors = ref([]);
const pointer = reactive({ x: 0, y: 0, visible: false });
let lastSpawn = 0;
let sequence = 0;

const spawnMeteor = (event, burst = false) => {
  const now = performance.now();
  if (!burst && now - lastSpawn < 34) return;
  lastSpawn = now;

  const amount = burst ? 7 : 1;
  for (let index = 0; index < amount; index += 1) {
    const id = sequence++;
    meteors.value.push({
      id,
      x: event.clientX + (burst ? Math.random() * 20 - 10 : 0),
      y: event.clientY + (burst ? Math.random() * 20 - 10 : 0),
      size: burst ? Math.random() * 4 + 4 : Math.random() * 3 + 3,
      rotate: burst ? Math.random() * 360 : -38,
    });
    window.setTimeout(() => {
      meteors.value = meteors.value.filter((meteor) => meteor.id !== id);
    }, 720);
  }
};

const handleMove = (event) => {
  pointer.x = event.clientX;
  pointer.y = event.clientY;
  pointer.visible = true;
  spawnMeteor(event);
};
const handleClick = (event) => spawnMeteor(event, true);
const hidePointer = () => (pointer.visible = false);

onMounted(() => {
  if (window.matchMedia("(pointer: fine)").matches) {
    window.addEventListener("pointermove", handleMove, { passive: true });
    window.addEventListener("pointerdown", handleClick, { passive: true });
    document.documentElement.classList.add("meteor-enabled");
    document.addEventListener("mouseleave", hidePointer);
  }
});

onBeforeUnmount(() => {
  window.removeEventListener("pointermove", handleMove);
  window.removeEventListener("pointerdown", handleClick);
  document.removeEventListener("mouseleave", hidePointer);
  document.documentElement.classList.remove("meteor-enabled");
});
</script>
