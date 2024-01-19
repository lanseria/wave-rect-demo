<script setup lang="ts">
const percentage = ref(100)
const ContainerRef = shallowRef()
const { height } = useElementSize(ContainerRef)
function handleAddPercent() {
  if (percentage.value < 100)
    percentage.value++
  else
    percentage.value = 0
}
const waveHeight = computed(() => {
  return (height.value - 8) * (percentage.value / 100)
})
</script>

<template>
  <div class="h-full w-full flex flex-col items-center justify-center bg-green-5">
    <div class="relative h-250px w-130px border-4px border-white rounded-25px border-solid">
      <div
        ref="ContainerRef"
        class="m-4px h-[calc(100%-8px)] overflow-hidden rounded-18px after:absolute after:left-43px after:top--18px after:h-10px after:w-40px after:rounded-tl-5px after:rounded-tr-5px after:bg-white after:content-['']"
      >
        <div class="h-full flex flex-col-reverse">
          <div
            class="h-[var(--height)] w-full shrink-0 bg-white transition-height duration-1000 ease-in-out" :style="{
              '--height': `${waveHeight}px`,
            }"
          />

          <svg
            class="mb--1px block h-10px w-full overflow-hidden"
            xmlns="http://www.w3.org/2000/svg"
            xmlns:xlink="http://www.w3.org/1999/xlink"
            viewBox="0 24 150 28"
            preserveAspectRatio="none"
          >
            <defs>
              <path
                id="gentle-wave"
                d="M-160 44c30 0 58-18 88-18s 58 18 88 18 58-18 88-18 58 18 88 18 v44h-352z"
              />
            </defs>
            <g class="parallax">
              <use xlink:href="#gentle-wave" x="50" y="0" fill="rgba(255, 255, 255, 0.6)" />
              <use xlink:href="#gentle-wave" x="50" y="3" fill="rgba(255, 255, 255, 0.8)" />
              <use xlink:href="#gentle-wave" x="50" y="6" fill="rgba(255, 255, 255, 1)" />
            </g>
          </svg>
        </div>
      </div>
    </div>

    <div class="mt-15px flex items-center text-white font-bold" @click="handleAddPercent">
      <div class="i-carbon-plug font-bold" /><span id="percentage">{{ percentage }}</span>%
    </div>
  </div>
</template>

<style lang="css" scoped>
.parallax > use {
  animation: move-forever 12s linear infinite;
  &:nth-child(1) {
    animation-delay: -2s;
    fill: rgba(255, 255, 255, 0.6);
  }
  &:nth-child(2) {
    animation-delay: -2s;
    animation-duration: 5s;
    fill: rgba(255, 255, 255, 0.8);
  }
  &:nth-child(3) {
    animation-delay: -4s;
    animation-duration: 3s;
    fill: rgba(255, 255, 255, 1);
  }
}

@keyframes move-forever {
  0% {
    transform: translate(-90px, 0%);
  }
  100% {
    transform: translate(85px, 0%);
  }
}
</style>
