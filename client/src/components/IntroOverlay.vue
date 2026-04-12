<template>
  <transition name="intro-fade">
    <div
      v-if="visible"
      class="intro-overlay"
      :class="{ 'intro-overlay--leaving': isLeaving }"
      aria-hidden="true"
    >
      <div class="intro-overlay__bg"></div>
      <div class="intro-overlay__vignette"></div>
      <div class="intro-overlay__noise"></div>

      <div class="intro-overlay__stage">
        <div class="intro-overlay__aura intro-overlay__aura--white"></div>
        <div class="intro-overlay__aura intro-overlay__aura--blue"></div>

        <div class="intro-overlay__wordmark-shell">
          <div class="intro-overlay__wordmark intro-overlay__wordmark--ghost"></div>
          <div class="intro-overlay__wordmark intro-overlay__wordmark--white"></div>
          <div class="intro-overlay__wordmark intro-overlay__wordmark--blue"></div>
        </div>
      </div>
    </div>
  </transition>
</template>

<script setup>
import { onBeforeUnmount, onMounted, ref } from 'vue'

const emit = defineEmits(['complete'])

const visible = ref(true)
const isLeaving = ref(false)

let leaveTimer = 0
let completeTimer = 0

onMounted(() => {
  leaveTimer = window.setTimeout(() => {
    isLeaving.value = true
  }, 3200)

  completeTimer = window.setTimeout(() => {
    visible.value = false
    emit('complete')
  }, 4050)
})

onBeforeUnmount(() => {
  window.clearTimeout(leaveTimer)
  window.clearTimeout(completeTimer)
})
</script>

<style scoped>
.intro-overlay {
  position: fixed;
  inset: 0;
  z-index: 100;
  overflow: hidden;
  display: flex;
  align-items: center;
  justify-content: center;
  background:
    radial-gradient(circle at 50% 44%, rgba(206, 232, 255, 0.09) 0%, rgba(146, 191, 255, 0.04) 22%, rgba(19, 19, 31, 0) 48%),
    linear-gradient(180deg, #090b12 0%, #0d1018 36%, #11131d 100%);
  isolation: isolate;
}

.intro-overlay__bg,
.intro-overlay__vignette,
.intro-overlay__noise,
.intro-overlay__aura,
.intro-overlay__wordmark {
  position: absolute;
  inset: 0;
  pointer-events: none;
}

.intro-overlay__bg {
  background:
    radial-gradient(circle at 50% 46%, rgba(255, 255, 255, 0.075) 0%, rgba(255, 255, 255, 0.028) 18%, rgba(255, 255, 255, 0) 44%),
    radial-gradient(circle at 50% 46%, rgba(79, 167, 255, 0.18) 0%, rgba(79, 167, 255, 0.08) 24%, rgba(79, 167, 255, 0) 58%);
  animation: introBackdrop 3.15s ease-out forwards;
}

.intro-overlay__vignette {
  background: radial-gradient(circle at center, rgba(0, 0, 0, 0) 38%, rgba(4, 8, 18, 0.82) 100%);
}

.intro-overlay__noise {
  opacity: 0.1;
  background-image:
    linear-gradient(rgba(255, 255, 255, 0.018) 1px, transparent 1px),
    linear-gradient(90deg, rgba(255, 255, 255, 0.018) 1px, transparent 1px);
  background-size: 56px 56px;
  mask-image: radial-gradient(circle at center, rgba(0, 0, 0, 0.95) 0%, rgba(0, 0, 0, 0.35) 60%, transparent 86%);
}

.intro-overlay__stage {
  position: relative;
  width: min(84vw, 1000px);
  min-height: 240px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.intro-overlay__aura {
  inset: 50% auto auto 50%;
  transform: translate(-50%, -50%);
  width: min(72vw, 820px);
  aspect-ratio: 2.35 / 1;
  border-radius: 999px;
  mix-blend-mode: screen;
}

.intro-overlay__aura--white {
  background: radial-gradient(circle at center, rgba(255, 255, 255, 0.42) 0%, rgba(255, 255, 255, 0.12) 32%, rgba(255, 255, 255, 0) 72%);
  filter: blur(36px);
  opacity: 0;
  animation: introWhiteAura 1.6s cubic-bezier(0.16, 0.84, 0.26, 1) forwards;
}

.intro-overlay__aura--blue {
  background: radial-gradient(circle at center, rgba(97, 196, 255, 0.34) 0%, rgba(53, 135, 255, 0.18) 38%, rgba(53, 135, 255, 0) 76%);
  filter: blur(30px);
  opacity: 0;
  animation: introBlueAura 1.8s cubic-bezier(0.18, 0.82, 0.22, 1) 1.32s forwards;
}

.intro-overlay__wordmark-shell {
  position: relative;
  width: min(76vw, 920px);
  aspect-ratio: 198 / 32;
}

.intro-overlay__wordmark {
  --wordmark-mask: url('/images/savvy-wordmark.svg');
  -webkit-mask-image: var(--wordmark-mask);
  mask-image: var(--wordmark-mask);
  -webkit-mask-repeat: no-repeat;
  mask-repeat: no-repeat;
  -webkit-mask-size: contain;
  mask-size: contain;
  -webkit-mask-position: center;
  mask-position: center;
  transform-origin: center;
}

.intro-overlay__wordmark--ghost {
  background: linear-gradient(180deg, rgba(255, 255, 255, 0.95) 0%, rgba(226, 238, 255, 0.92) 100%);
  opacity: 0;
  filter: blur(38px);
  transform: scale(1.12);
  animation: introGhostGather 1.55s cubic-bezier(0.16, 0.84, 0.28, 1) forwards;
}

.intro-overlay__wordmark--white {
  background: linear-gradient(180deg, rgba(255, 255, 255, 1) 0%, rgba(247, 251, 255, 0.98) 45%, rgba(226, 238, 255, 0.94) 100%);
  opacity: 0;
  filter: blur(34px) brightness(1.24);
  transform: scale(1.08);
  animation:
    introWhiteReveal 1.55s cubic-bezier(0.16, 0.84, 0.28, 1) forwards,
    introWhiteToHighlight 1.4s ease-out 1.45s forwards;
}

.intro-overlay__wordmark--blue {
  background:
    linear-gradient(180deg, #f7fbff 0%, #e5f4ff 18%, #8dd6ff 55%, #58b7ff 76%, #2d73ff 100%),
    linear-gradient(90deg, #f6fbff 0%, #d8ecff 23%, #96d8ff 52%, #49b2ff 74%, #2e73ff 100%);
  background-blend-mode: screen, normal;
  opacity: 0;
  filter: blur(20px) saturate(0.92);
  transform: scale(1.035);
  animation: introBlueShift 1.65s cubic-bezier(0.18, 0.82, 0.22, 1) 1.32s forwards;
}

.intro-overlay--leaving {
  animation: introOverlayExit 0.78s cubic-bezier(0.55, 0, 0.45, 1) forwards;
}

.intro-fade-leave-active {
  transition: opacity 0.24s ease;
}

.intro-fade-leave-to {
  opacity: 0;
}

@keyframes introBackdrop {
  0% {
    opacity: 0.72;
    transform: scale(1.04);
  }
  100% {
    opacity: 1;
    transform: scale(1);
  }
}

@keyframes introGhostGather {
  0% {
    opacity: 0;
    filter: blur(42px);
    transform: scale(1.14);
  }
  28% {
    opacity: 0.26;
  }
  72% {
    opacity: 0.16;
    filter: blur(18px);
    transform: scale(1.04);
  }
  100% {
    opacity: 0;
    filter: blur(10px);
    transform: scale(1.01);
  }
}

@keyframes introWhiteReveal {
  0% {
    opacity: 0;
    filter: blur(36px) brightness(1.34);
    transform: scale(1.09);
  }
  20% {
    opacity: 0.05;
  }
  58% {
    opacity: 0.92;
    filter: blur(8px) brightness(1.18);
  }
  100% {
    opacity: 1;
    filter: blur(0) brightness(1);
    transform: scale(1);
  }
}

@keyframes introWhiteToHighlight {
  0% {
    opacity: 1;
    filter: blur(0) brightness(1);
  }
  100% {
    opacity: 0.24;
    filter: blur(0.35px) brightness(1.08);
  }
}

@keyframes introBlueShift {
  0% {
    opacity: 0;
    filter: blur(18px) saturate(0.86);
    transform: scale(1.04);
  }
  18% {
    opacity: 0.08;
  }
  58% {
    opacity: 0.74;
    filter: blur(5px) saturate(1.06);
  }
  100% {
    opacity: 1;
    filter: blur(0) saturate(1.12);
    transform: scale(1);
  }
}

@keyframes introWhiteAura {
  0% {
    opacity: 0;
    transform: translate(-50%, -50%) scale(0.78);
  }
  48% {
    opacity: 0.9;
  }
  100% {
    opacity: 0.28;
    transform: translate(-50%, -50%) scale(1);
  }
}

@keyframes introBlueAura {
  0% {
    opacity: 0;
    transform: translate(-50%, -50%) scale(0.9);
  }
  58% {
    opacity: 0.76;
  }
  100% {
    opacity: 0.44;
    transform: translate(-50%, -50%) scale(1.02);
  }
}

@keyframes introOverlayExit {
  0% {
    opacity: 1;
    filter: blur(0);
    transform: scale(1);
  }
  100% {
    opacity: 0;
    filter: blur(10px);
    transform: scale(1.015);
  }
}

@media (max-width: 768px) {
  .intro-overlay__stage {
    width: min(92vw, 720px);
    min-height: 180px;
  }

  .intro-overlay__wordmark-shell {
    width: min(90vw, 720px);
  }

  .intro-overlay__noise {
    background-size: 38px 38px;
  }
}

@media (prefers-reduced-motion: reduce) {
  .intro-overlay,
  .intro-overlay *,
  .intro-fade-leave-active {
    animation-duration: 0.01ms !important;
    animation-delay: 0ms !important;
    transition-duration: 0.01ms !important;
  }
}
</style>
