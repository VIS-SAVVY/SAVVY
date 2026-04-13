<template>
  <div class="intro-overlay" aria-hidden="true">
    <div class="intro-overlay__glow" :class="{ 'intro-overlay__glow--ready': isReady }"></div>

    <div class="intro-overlay__stage" :class="{ 'intro-overlay__stage--ready': isReady }">
      <div v-if="showWordmark" class="intro-wordmark">
        <div class="intro-wordmark__savvy" aria-label="Savvy">
          <span class="intro-wordmark__text intro-wordmark__text--savvy intro-wordmark__text--savvy-shadow">
            {{ savvyText }}
          </span>
          <span class="intro-wordmark__text intro-wordmark__text--savvy intro-wordmark__text--savvy-main">
            {{ savvyText }}
          </span>
          <span class="intro-wordmark__text intro-wordmark__text--savvy intro-wordmark__text--savvy-fill">
            {{ savvyText }}
          </span>
          <span class="intro-wordmark__text intro-wordmark__text--savvy intro-wordmark__text--savvy-glow">
            {{ savvyText }}
          </span>
        </div>

        <div class="intro-wordmark__vis" aria-label="VIS2026">
          <span class="intro-wordmark__text intro-wordmark__text--vis intro-wordmark__text--vis-shadow">
            {{ visText }}
          </span>
          <span class="intro-wordmark__text intro-wordmark__text--vis intro-wordmark__text--vis-main">
            {{ visText }}
          </span>
          <span class="intro-wordmark__text intro-wordmark__text--vis intro-wordmark__text--vis-fill">
            {{ visText }}
          </span>
          <span class="intro-wordmark__text intro-wordmark__text--vis intro-wordmark__text--vis-glow">
            {{ visText }}
          </span>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { onBeforeUnmount, onMounted, ref } from 'vue'

const emit = defineEmits(['complete'])

const DEFAULT_INTRO_DURATION_MS = 2800
const BASE_URL = import.meta.env.BASE_URL || '/'
const FONT_NAME = 'Rindu'
const savvyText = 'Savvy'
const visText = 'VIS2026'
const isDebugFreeze = typeof window !== 'undefined' && new URLSearchParams(window.location.search).has('introDebug')
const introDurationMs = isDebugFreeze ? 120000 : DEFAULT_INTRO_DURATION_MS

const withBase = (relativePath) => new URL(relativePath, window.location.origin + BASE_URL).toString()

const isReady = ref(false)
const showWordmark = ref(false)

let completeTimer = null
let mountFrame = 0
let readyFrame = 0

const loadIntroFont = async () => {
  if (typeof window === 'undefined' || !('FontFace' in window)) {
    return
  }

  if (!document.fonts?.check?.(`1em "${FONT_NAME}"`)) {
    try {
      const font = new FontFace(FONT_NAME, `url(${withBase('fonts/rindu-demo-2.ttf')}) format("truetype")`)
      await font.load()
      document.fonts.add(font)
    } catch (error) {
      console.error('Unable to load intro font.', error)
    }
  }

  if (document.fonts?.load) {
    await document.fonts.load(`1em "${FONT_NAME}"`)
  }

  if (document.fonts?.ready) {
    await document.fonts.ready
  }
}

onMounted(async () => {
  await loadIntroFont()

  mountFrame = window.requestAnimationFrame(() => {
    showWordmark.value = true

    readyFrame = window.requestAnimationFrame(() => {
      isReady.value = true

      completeTimer = window.setTimeout(() => {
        emit('complete')
      }, introDurationMs)
    })
  })
})

onBeforeUnmount(() => {
  if (mountFrame) {
    window.cancelAnimationFrame(mountFrame)
  }

  if (readyFrame) {
    window.cancelAnimationFrame(readyFrame)
  }

  if (completeTimer !== null) {
    window.clearTimeout(completeTimer)
  }
})
</script>

<style scoped>
@font-face {
  font-family: 'Rindu';
  src: url('/fonts/rindu-demo-2.ttf') format('truetype');
  font-style: normal;
  font-weight: 400;
  font-display: block;
}

.intro-overlay {
  position: fixed;
  inset: 0;
  z-index: 100;
  display: flex;
  align-items: center;
  justify-content: center;
  width: 100%;
  height: 100%;
  background:
    radial-gradient(circle at 50% 42%, rgba(27, 40, 57, 0.58) 0%, rgba(17, 25, 35, 0.22) 35%, rgba(11, 17, 25, 0) 72%),
    linear-gradient(180deg, #141d27 0%, #0d141c 100%);
  overflow: hidden;
}

.intro-overlay__glow {
  position: absolute;
  inset: 0;
  opacity: 0;
  transform: scale(0.97);
  background:
    radial-gradient(circle at 50% 44%, rgba(24, 139, 255, 0) 0%, rgba(24, 139, 255, 0) 16%, rgba(24, 139, 255, 0) 28%, rgba(24, 139, 255, 0) 100%);
}

.intro-overlay__glow--ready {
  animation: introBackdropGlow 1850ms cubic-bezier(0.22, 0.78, 0.24, 1) forwards;
}

.intro-overlay__stage {
  position: relative;
  display: flex;
  align-items: center;
  justify-content: center;
  width: min(100vw, 1280px);
  min-height: min(100vh, 820px);
  padding: clamp(10px, 2vw, 28px);
  opacity: 0;
  overflow: visible;
}

.intro-overlay__stage--ready {
  opacity: 1;
}

.intro-wordmark {
  position: relative;
  display: inline-flex;
  align-items: flex-start;
  justify-content: center;
  isolation: isolate;
  overflow: visible;
}

.intro-wordmark__savvy,
.intro-wordmark__vis {
  position: relative;
  display: inline-block;
  overflow: visible;
}

.intro-wordmark__savvy {
  padding: 0.03em 0.04em 0.28em 0.04em;
  line-height: 1.08;
}

.intro-wordmark__vis {
  position: absolute;
  right: clamp(0.05em, 1vw, 0.22em);
  top: clamp(-0.24em, -0.92vw, -0.13em);
}

.intro-wordmark__text {
  display: inline-block;
  white-space: nowrap;
  font-family: 'Rindu', 'Brush Script MT', 'Segoe Script', cursive;
  font-style: normal;
  font-weight: 400;
  letter-spacing: 0;
  backface-visibility: hidden;
  will-change: opacity, color, filter, transform, clip-path;
}

.intro-wordmark__text--savvy {
  font-size: clamp(10.8rem, 33vw, 23rem);
}

.intro-wordmark__text--vis {
  font-size: clamp(2.95rem, 6.3vw, 5.1rem);
  line-height: 1;
}

.intro-wordmark__text--savvy-shadow,
.intro-wordmark__text--vis-shadow {
  position: relative;
  color: #13202c;
  opacity: 0;
  filter: blur(5px);
  transform: translateY(0.12em) scale(0.988);
}

.intro-wordmark__text--savvy-main,
.intro-wordmark__text--savvy-fill,
.intro-wordmark__text--savvy-glow,
.intro-wordmark__text--vis-main,
.intro-wordmark__text--vis-fill,
.intro-wordmark__text--vis-glow {
  position: absolute;
  inset: 0;
  opacity: 0;
}

.intro-wordmark__text--savvy-main,
.intro-wordmark__text--vis-main {
  color: #ffffff;
  filter: blur(4px);
  transform: translateY(0.08em) scale(0.994);
  clip-path: inset(72% 0 0 0);
}

.intro-wordmark__text--savvy-fill,
.intro-wordmark__text--vis-fill {
  color: #178bff;
  filter: blur(4px);
  transform: translateY(0.08em) scale(0.994);
  clip-path: inset(100% 0 0 0);
}

.intro-wordmark__text--savvy-glow,
.intro-wordmark__text--vis-glow {
  color: #dfefff;
  filter: blur(9px);
  transform: translateY(0.05em);
  mix-blend-mode: screen;
}

.intro-overlay__stage--ready .intro-wordmark__text--savvy-shadow {
  animation: introShadowInk 860ms cubic-bezier(0.22, 0.8, 0.25, 1) forwards;
}

.intro-overlay__stage--ready .intro-wordmark__text--savvy-main {
  animation: introSweepReveal 780ms cubic-bezier(0.22, 0.8, 0.24, 1) 20ms forwards;
}

.intro-overlay__stage--ready .intro-wordmark__text--savvy-fill {
  animation: introBlueFlood 1120ms cubic-bezier(0.22, 0.82, 0.24, 1) 180ms forwards;
}

.intro-overlay__stage--ready .intro-wordmark__text--savvy-glow {
  animation: introGlowBloom 480ms ease-out 760ms forwards;
}

.intro-overlay__stage--ready .intro-wordmark__text--vis-shadow {
  animation: introShadowInk 620ms cubic-bezier(0.22, 0.8, 0.25, 1) 420ms forwards;
}

.intro-overlay__stage--ready .intro-wordmark__text--vis-main {
  animation: introSweepReveal 520ms cubic-bezier(0.22, 0.8, 0.24, 1) 480ms forwards;
}

.intro-overlay__stage--ready .intro-wordmark__text--vis-fill {
  animation: introBlueFlood 760ms cubic-bezier(0.22, 0.82, 0.26, 1) 590ms forwards;
}

.intro-overlay__stage--ready .intro-wordmark__text--vis-glow {
  animation: introGlowBloom 420ms ease-out 980ms forwards;
}

:global(.intro-fade-leave-active) {
  transition: opacity 0.4s ease;
}

:global(.intro-fade-leave-from) {
  opacity: 1;
}

:global(.intro-fade-leave-to) {
  opacity: 0;
}

@keyframes introBackdropGlow {
  0% {
    opacity: 0;
    transform: scale(0.97);
  }
  52% {
    opacity: 0.34;
    transform: scale(1);
    background:
      radial-gradient(circle at 50% 44%, rgba(24, 139, 255, 0.045) 0%, rgba(24, 139, 255, 0.038) 18%, rgba(24, 139, 255, 0.014) 32%, rgba(24, 139, 255, 0) 74%);
  }
  100% {
    opacity: 0.58;
    transform: scale(1.03);
    background:
      radial-gradient(circle at 50% 44%, rgba(24, 139, 255, 0.072) 0%, rgba(24, 139, 255, 0.05) 20%, rgba(24, 139, 255, 0.018) 36%, rgba(24, 139, 255, 0) 76%);
  }
}

@keyframes introShadowInk {
  0% {
    opacity: 0;
    color: #0f151c;
    filter: blur(9px);
    transform: translateY(0.13em) scale(0.986);
  }
  42% {
    opacity: 0.1;
  }
  100% {
    opacity: 0.22;
    color: #162431;
    filter: blur(1.8px);
    transform: translateY(0.03em) scale(0.998);
  }
}

@keyframes introSweepReveal {
  0% {
    opacity: 0;
    filter: blur(6px);
    transform: translateY(0.08em) scale(0.994);
    clip-path: inset(72% 0 0 0);
  }
  18% {
    opacity: 0.12;
    clip-path: inset(60% 0 0 0);
  }
  54% {
    opacity: 0.62;
    filter: blur(2.2px);
    transform: translateY(0.03em) scale(0.998);
    clip-path: inset(24% 0 0 0);
  }
  100% {
    opacity: 1;
    filter: blur(0);
    transform: translateY(0) scale(1);
    clip-path: inset(0 0 0 0);
  }
}

@keyframes introBlueFlood {
  0% {
    opacity: 0;
    filter: blur(5px);
    transform: translateY(0.08em) scale(0.994);
    clip-path: inset(100% 0 0 0);
  }
  18% {
    opacity: 0.18;
    clip-path: inset(78% 0 0 0);
  }
  52% {
    opacity: 0.74;
    filter: blur(2.1px);
    transform: translateY(0.03em) scale(0.998);
    clip-path: inset(34% 0 0 0);
  }
  100% {
    opacity: 1;
    filter: blur(0);
    transform: translateY(0) scale(1);
    clip-path: inset(0 0 0 0);
  }
}

@keyframes introGlowBloom {
  0% {
    opacity: 0;
    filter: blur(10px);
    transform: translateY(0.04em) scale(0.997);
  }
  60% {
    opacity: 0.18;
    filter: blur(6px);
  }
  100% {
    opacity: 0.22;
    filter: blur(2px);
    transform: translateY(0) scale(1);
  }
}
</style>
