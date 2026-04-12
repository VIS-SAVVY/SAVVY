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
      <div class="intro-overlay__grid"></div>

      <div class="intro-overlay__stage">
        <div class="intro-overlay__halo"></div>
        <div class="intro-overlay__wordmark-shell">
          <div class="intro-overlay__wordmark intro-overlay__wordmark--white"></div>
          <div class="intro-overlay__wordmark intro-overlay__wordmark--gradient"></div>
          <div class="intro-overlay__wordmark intro-overlay__wordmark--outline"></div>
          <span class="intro-overlay__sheen"></span>
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
  }, 2850)

  completeTimer = window.setTimeout(() => {
    visible.value = false
    emit('complete')
  }, 3650)
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
    radial-gradient(circle at 50% 42%, rgba(141, 186, 255, 0.14) 0%, rgba(141, 186, 255, 0.02) 30%, rgba(19, 19, 31, 0) 58%),
    linear-gradient(160deg, #0a0f18 0%, #101728 34%, #13131f 70%, #0c1425 100%);
  isolation: isolate;
}

.intro-overlay__bg,
.intro-overlay__vignette,
.intro-overlay__grid {
  position: absolute;
  inset: 0;
  pointer-events: none;
}

.intro-overlay__bg {
  background:
    radial-gradient(circle at 50% 45%, rgba(220, 235, 255, 0.16) 0%, rgba(220, 235, 255, 0.04) 24%, rgba(220, 235, 255, 0) 58%),
    radial-gradient(circle at 50% 50%, rgba(255, 255, 255, 0.04) 0%, rgba(255, 255, 255, 0) 62%);
  animation: introPulse 3.05s ease-out forwards;
}

.intro-overlay__vignette {
  background: radial-gradient(circle at center, rgba(0, 0, 0, 0) 42%, rgba(4, 8, 18, 0.78) 100%);
}

.intro-overlay__grid {
  background-image:
    linear-gradient(rgba(163, 189, 255, 0.05) 1px, transparent 1px),
    linear-gradient(90deg, rgba(163, 189, 255, 0.05) 1px, transparent 1px);
  background-size: 48px 48px;
  mask-image: radial-gradient(circle at center, rgba(0, 0, 0, 0.8) 0%, rgba(0, 0, 0, 0.22) 54%, transparent 82%);
  opacity: 0;
  animation: introGrid 3s ease forwards;
}

.intro-overlay__stage {
  position: relative;
  width: min(82vw, 980px);
  min-height: 240px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.intro-overlay__halo {
  position: absolute;
  inset: 50% auto auto 50%;
  width: min(68vw, 760px);
  aspect-ratio: 2.2 / 1;
  transform: translate(-50%, -50%);
  background: radial-gradient(circle at center, rgba(124, 174, 255, 0.34) 0%, rgba(89, 142, 255, 0.16) 34%, rgba(31, 67, 135, 0) 74%);
  filter: blur(22px);
  opacity: 0;
  animation: introHalo 2.5s ease forwards;
}

.intro-overlay__wordmark-shell {
  position: relative;
  width: min(74vw, 920px);
  aspect-ratio: 198 / 32;
  overflow: hidden;
}

.intro-overlay__wordmark,
.intro-overlay__sheen {
  position: absolute;
  inset: 0;
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

.intro-overlay__wordmark--white {
  background: linear-gradient(180deg, rgba(255, 255, 255, 0.98) 0%, rgba(241, 247, 255, 0.96) 48%, rgba(215, 231, 255, 0.9) 100%);
  opacity: 0;
  filter: blur(26px) drop-shadow(0 0 0 rgba(255, 255, 255, 0));
  transform: scale(1.05);
  animation: introWhiteReveal 1.45s cubic-bezier(0.18, 0.8, 0.24, 1) forwards;
}

.intro-overlay__wordmark--gradient {
  background:
    linear-gradient(180deg, rgba(255, 255, 255, 0.95) 0%, rgba(226, 236, 255, 0.92) 22%, rgba(176, 205, 255, 0.96) 44%, rgba(115, 165, 255, 0.98) 68%, rgba(69, 122, 235, 0.98) 100%),
    linear-gradient(90deg, #eef4ff 0%, #d8e7ff 20%, #f7fbff 38%, #8cb8ff 58%, #4f86ea 80%, #84a3ea 100%);
  background-blend-mode: screen, normal;
  opacity: 0;
  filter: blur(22px) drop-shadow(0 0 8px rgba(142, 187, 255, 0.12));
  transform: scale(1.035);
  clip-path: inset(0 0 100% 0);
  animation: introGradientFill 1.7s cubic-bezier(0.22, 0.86, 0.2, 1) 0.82s forwards;
}

.intro-overlay__wordmark--outline {
  background: linear-gradient(180deg, rgba(255, 255, 255, 0.22) 0%, rgba(160, 192, 255, 0.24) 100%);
  opacity: 0;
  filter: blur(0.5px);
  transform: scale(1.002);
  animation: introOutlineIn 0.9s ease 1.35s forwards;
}

.intro-overlay__sheen {
  background: linear-gradient(108deg, transparent 18%, rgba(255, 255, 255, 0.05) 42%, rgba(255, 255, 255, 0.82) 50%, rgba(255, 255, 255, 0.09) 58%, transparent 84%);
  transform: translateX(-128%) skewX(-18deg);
  mix-blend-mode: screen;
  opacity: 0;
  animation: introSheen 1.15s ease 1.22s forwards;
}

.intro-overlay--leaving {
  animation: introOverlayExit 0.72s cubic-bezier(0.55, 0, 0.45, 1) forwards;
}

.intro-fade-leave-active {
  transition: opacity 0.25s ease;
}

.intro-fade-leave-to {
  opacity: 0;
}

@keyframes introWhiteReveal {
  0% {
    opacity: 0;
    filter: blur(34px) drop-shadow(0 0 0 rgba(255, 255, 255, 0));
    transform: scale(1.07);
  }
  42% {
    opacity: 0.96;
  }
  100% {
    opacity: 1;
    filter: blur(0) drop-shadow(0 0 26px rgba(232, 242, 255, 0.2));
    transform: scale(1);
  }
}

@keyframes introGradientFill {
  0% {
    opacity: 0;
    clip-path: inset(0 0 100% 0);
    filter: blur(22px) drop-shadow(0 0 8px rgba(142, 187, 255, 0.12));
    transform: scale(1.03);
  }
  25% {
    opacity: 0.34;
  }
  62% {
    opacity: 0.88;
    clip-path: inset(0 0 18% 0);
    filter: blur(6px) drop-shadow(0 0 18px rgba(122, 170, 255, 0.18));
  }
  100% {
    opacity: 1;
    clip-path: inset(0 0 0 0);
    filter: blur(0) drop-shadow(0 0 24px rgba(122, 170, 255, 0.2));
    transform: scale(1);
  }
}

@keyframes introOutlineIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 0.46;
  }
}

@keyframes introHalo {
  0% {
    opacity: 0;
    transform: translate(-50%, -50%) scale(0.7);
  }
  46% {
    opacity: 1;
  }
  100% {
    opacity: 0.88;
    transform: translate(-50%, -50%) scale(1);
  }
}

@keyframes introPulse {
  0% {
    opacity: 0.2;
    transform: scale(1.08);
  }
  100% {
    opacity: 1;
    transform: scale(1);
  }
}

@keyframes introGrid {
  0% {
    opacity: 0;
    transform: scale(1.06);
  }
  40% {
    opacity: 0.18;
  }
  100% {
    opacity: 0.12;
    transform: scale(1);
  }
}

@keyframes introSheen {
  0% {
    opacity: 0;
    transform: translateX(-128%) skewX(-18deg);
  }
  18% {
    opacity: 0.92;
  }
  100% {
    opacity: 0;
    transform: translateX(132%) skewX(-18deg);
  }
}

@keyframes introOverlayExit {
  0% {
    opacity: 1;
  }
  100% {
    opacity: 0;
    transform: scale(1.016);
    filter: blur(8px);
  }
}

@media (max-width: 768px) {
  .intro-overlay__stage {
    width: min(90vw, 720px);
    min-height: 180px;
  }

  .intro-overlay__wordmark-shell {
    width: min(88vw, 720px);
  }

  .intro-overlay__grid {
    background-size: 36px 36px;
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
